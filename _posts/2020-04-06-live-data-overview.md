---
layout:   post
title:    "Android 架构组件之 LiveData"
date:     2020-04-06
author:   "Eric"
header-img: "img/post/bg/post-bg-android.png"
catalog:  true
tags:
  - Android
  - 架构组件
---

## 1. 来源
继 2015 年 Google IO 大会推出 Data Binding 后，2017 年 Google IO 大会上，**推出 Android 的 4 大架构组件：Lifecycle，LiveData，ViewModel，Room**。

![android-architecture-component][1]

在下一年也就是 2018 年，Google IO 大会发布了一个优质的工具库 [Jetpack](https://developer.android.google.cn/jetpack/)。Jetpack 将 Data Binding、4 大架构组件与新加入的 Navigation、Paging、WorkManager整合为 Jetpack 的架构系组件。

![jetpack-overview][2]

LiveData 是 Jetpack 架构系列组件中的核心一员。它的职责是当数据变更时，及时地通知视图。它采用观察者模式，与 EvenBus 有相通之处。

## 2. 与 Lifecycle 的关系
在 `Support Library 26.1.0` 之后，AppCompatActivity、Fragment 就实现了 LifecycleOwner。

```java
public class ComponentActivity extends Activity implements LifecycleOwner {

}

public class FragmentActivity extends ComponentActivity {

}

public class AppCompatActivity extends FragmentActivity {
    
}

public class Fragment implements LifecycleOwner {

}
```

**`Lifecycle` 是一个生命周期感知组件**。
`Lifecycle` 能够：
- 实时提供 Activity/Fragment 的当前生命周期状态
- 支持监听 Activity/Fragment 生命周期中各事件

```java
/**
 * Lifecycle拥有者
 */
public interface LifecycleOwner {
    @NonNull
    Lifecycle getLifecycle();
}

/**
 * LifecycleEvent 事件观察者
 */
public interface LifecycleEventObserver extends LifecycleObserver {
    void onStateChanged(@NonNull LifecycleOwner source, @NonNull Lifecycle.Event event);
}

/**
 * Lifecycle 抽象类
 */
public abstract class Lifecycle {
    @MainThread
    public abstract void addObserver(@NonNull LifecycleObserver observer);

    @MainThread
    public abstract void removeObserver(@NonNull LifecycleObserver observer);

    @MainThread
    @NonNull
    public abstract State getCurrentState();
}
```

`Lifecycle` 对 `LiveData` 提供了生命周期感知能力，避免了 Activity/Fragment 的内存泄漏问题。

## 3. 主要方法和内部类
```java
public abstract class LiveData<T> {
    /**
     * 添加一个生命周期感知的观察者
     */
    @MainThread
    public void observe(@NonNull LifecycleOwner owner, @NonNull Observer<? super T> observer) {
    }

    /**
     * 移除与 Lifecycle 持有者关联的所有观察者
     */
    @MainThread
    public void removeObservers(@NonNull final LifecycleOwner owner) {

    /**
     * 添加永久观察者
     */
    @MainThread
    public void observeForever(@NonNull Observer<? super T> observer) {
    }

    /**
     * 移除观察者
     */
    @MainThread
    public void removeObserver(@NonNull final Observer<? super T> observer) {
    }

    /**
     * 更新数据（可在 MainThread、WorkThread）
     */
    protected void postValue(T value) {
    }

    /**
     * 更新数据（仅可在 MainThread）
     */
    @MainThread
    protected void setValue(T value) {
    }

    /**
     * 获取最新数据
     */
    @Nullable
    public T getValue() {
    }

    /**
     * 观察者包装类
     */
    private abstract class ObserverWrapper {
    }

    /**
     * 受 Lifecycle 约束的观察者
     */
    class LifecycleBoundObserver extends ObserverWrapper implements GenericLifecycleObserver {
    }

    /**
     * 永久活跃观察者
     */
    private class AlwaysActiveObserver extends ObserverWrapper {
    }
}
```

## 4. 使用
如果要实现：
1. 刚进入界面时，先获取数据库的数据来刷新界面，然后获取云端数据来刷新界面
2. 点击界面上的按钮，触发一次访问云端数据，然后刷新界面

可以按照如下步骤来编码。
### 4.1 以数据库作为数据源的数据仓
```java
public class DatabaseRepo {
    private MutableLiveData<Data> mData = new MutableLiveData<>();

    public LiveData<Data> getLiveData() {
        return mData;
    }

    public void triggerUpdate() {
        AsyncTask.execute(new Runnable() {
            @Override
            public void run() {
                // Access database to fetch data
                mData.postValue(new Data());
            }
        });
    }
}
```

### 4.2 以远（云）端作为数据源的数据仓
```java
public class RemoteRepo {
    private MutableLiveData<Data> mData = new MutableLiveData<>();
    private MutableLiveData<Response> mResponse = new MutableLiveData<>();

    public LiveData<Data> getData() {
        return mData;
    }

    public LiveData<Response> getResponse() {
        return mResponse;
    }

    public void triggerUpdate() {
        AsyncTask.execute(new Runnable() {
            @Override
            public void run() {
                // Access Remote to fetch new data
                mResponse.postValue(new Response());
                mData.postValue(new Data());
            }
        });
    }
}   
```

### 4.3 合并两个数据源为统一数据仓
```java
public class Repo {
    private DatabaseRepo mDatabaseRepo = new DatabaseRepo();
    private RemoteRepo mRemoteRepo = new RemoteRepo();
    private final MediatorLiveData<Data> mData;

    public Repo() {
        mData = new MediatorLiveData<>();
        mData.addSource(mDatabaseRepo.getLiveData(), new Observer<Data>() {
            @Override
            public void onChanged(Data data) {
                mData.setValue(data);
            }
        });
        mData.addSource(mRemoteRepo.getData(), new Observer<Data>() {
            @Override
            public void onChanged(Data data) {
                mData.setValue(data);
            }
        });
        mDatabaseRepo.triggerUpdate();
        mRemoteRepo.triggerUpdate();
    }

    public LiveData<Data> getData() {
        return mData;
    }

    public void triggerUpdate() {
        mRemoteRepo.triggerUpdate();
    }
}
```

### 4.4 在 Activity 中使用
```java
public class MainActivity extends AppCompatActivity {
    private Repo mRepo = new Repo();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mRepo.getData().observe(this, new Observer<Data>() {
            @Override
            public void onChanged(Data data) {
                // UI update
                Toast.makeText(MainActivity.this, "New data has come", Toast.LENGTH_SHORT);
            }
        });

        findViewById(R.id.hello_btn).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // click to trigger data repo update
                mRepo.triggerUpdate();
            }
        });
    }
}
```

## 5. 总结
`LiveData` 提供了一种 `WorkThread` 与 `MainThread` 沟通的新方式。其线程数据交换方式是基于 Handler 来实现的。除开 `Lifecycle` 提供的生命周期感知能力，`LiveData` 与 `EventBus` 有些类似，都是观察者模式的实现，都利用了 Handler 作为线程数据交换方式。但是，两者在用途上，却有着不同的定位。

![eventbus-vs-livedata][5]
- EventBus 是基于消息的，而 LiveData 是基于数据
- EventBus 是粗粒度的，而 LiveData 是细粒度
- EventBus 更使用于全局的、跨模块的消息通信，而 LiveData 适用于局部的、View 与 Model 间的数据解耦

最后再放一张图。

![android-application-architecture][6]

这是 Android 4 大架构组件推出的同时，Google 提出的`新型 Android 应用架构`，可以明显地看出 `LiveData` 在其中的核心地位。

[1]: /img/post/2019/post-live-data-overview/android-architecture-component.png
[2]: /img/post/2019/post-live-data-overview/jetpack-overview.jpg
[3]: /img/post/2019/post-live-data-overview/LifecycleOwner-source.png
[4]: /img/post/2019/post-live-data-overview/getLifecycle-call.png
[5]: /img/post/2019/post-live-data-overview/eventbus-vs-livedata.png
[6]: /img/post/2019/post-live-data-overview/android-application-architecture.png