---
layout:     post
title:      Android设计模式
subtitle:   MVP模式简单解读
date:       2018-11-12
author:     TkiChus
header-img: img/post-bg-mvp.jpg
catalog: true
tags:
    - TkiChus
    - DreamMemory001 Blog
    - Android
---
# MVP模式简单解析

     在Android的考法中，我们通常会将一个项目分成一个个的模块文件夹来进行管理维护，
     有的人是直接按照功能来分模块，这也是最常见的设计模式。但是有的人则会按照一定
    设计模式，再结合功能来进行项目模式的设计，比如现在常的MVP，MVVM这俩种目前比较
    流行的项目设计模式。本博客介绍的是MVP模式。


### MVP模式是由MVC模式逐渐演化出来的。我们首先进行一下对比

> MVC

M（model）模型, 是应用程序中用于处理应用数据逻辑的部分，
通常模型对象负责在数据库中进行存取

V(view)视图， 是应用程序中处理数据的显示部分，通常视图
是一句模型数据来创建的

C（controller）控制器， 是应用程序中处理用户交互的部分，
通常控制器负责从视图读取数据，控制用户的输入，并向模型发送
数据。

> MVP

MVP

M（model）负责数据的请求，解析，过滤等数据操作

V（View）负责图示部分展示，图示事件处理，Activity，
Fragment，Dialog，ViewGroup等呈现视图的组件都可以承担该
角色

P（presenter）是View和Model交互的桥梁

* MVP模式和MVC模式对比图

![](http://ww1.sinaimg.cn/large/006nBCHPly1fzsdttxqkcj30lm099t9l.jpg)

### 使用MVP的原因

在Android中，对于Activity并没有明确的说他是属于
View还是Controller的范畴，Activity既有View的性质
，也具有Controller的性质，所以导致MVC在Android中很
难明确分工使用，导致Activity很重。而且MVC中的View会
与Model直接交互，所以Activity与Model的耦合性很高，当
后期维护时，稍有变动，可能Model，Activity，XML都会跟
着改变，工作量很大，成本太高。

而MVP与MVC最大的不同之处，MVP将M和V分隔来，通过P交互，
这样在Android中，就可以明确的把Activity当做View处理，
虽然可能还有一点逻辑在其中，但是已经无伤大雅；View和Model
不直接交互，当View有变动或者Model有变动时，不会相互影响
，有太大变动，耦合性低，对于后期维护来说，特别是项目越来越庞大
时，可以很快的理清项目的结构，找到需要修改的地方，大大缩短
了工作量。而且， 因为View与Model分离的缘故，Model可以单独
进行单元测试。

所以，最后个人认为如果你的项目越来越庞大，不妨试试MVP+DataBing
，其实这就有点类似于MVP模式，方便快捷，即使项目庞大，改变时也
不需要太多重构。


### MVPLoader

> 下面是自己写的代码

```java
==================================View=======================================

所有的view（Activity、FragmentActivity、Fragment...）都必须实现这个接口

public interface IView {
    // 此方法是为了当Presenter中需要获取上下文对象时，传递上下文对象，而不是让Presenter直接持有上下  文对象
    Activity getSelfActivity();
}

这是Activity的基类：

public abstract class BaseActivity<P extends IPresenter> extends Activity implements IView {
    // Presenter对象
    protected P MvpPre;

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        MvpPre = bindPresenter();
    }

    // 绑定Presenter
    protected abstract P bindPresenter();

    public <T> T $(int resId) {
        return (T) findViewById(resId);
    }

    public <T> T $(int resId, View parent) {
        return (T) parent.findViewById(resId);
    }

    @Override
    public Activity getSelfActivity() {
        return this;
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        /**
         * 在生命周期结束时，将presenter与view之间的联系断开，防止出现内存泄露
         */
        if (MvpPre != null) {
            MvpPre.detachView();
        }
    }
}

==================================Presenter=======================================
public interface IPresenter {
    void detachView();
}

Presenter的基类：

public abstract class BasePresenter<V extends IView> implements IPresenter {
    // 此处使用弱引用是因为，有时Activity关闭不一定会走onDestroy，所以这时使用弱引用可以及时回收IView
    protected Reference<V> MvpRef;

    public BasePresenter(V view) {
        attachView(view);
    }

    private void attachView(V view) {
        MvpRef = new WeakReference<V>(view);
    }

    protected V getView() {
        if (MvpRef != null) {
            return MvpRef.get();
        }
        return null;
    }

    /**
     * 主要用于判断IView的生命周期是否结束，防止出现内存泄露状况
     *
     * @return
     */
    protected boolean isViewAttach() {
        return MvpRef != null && MvpRef.get() != null;
    }

    /**
     * Activity生命周期结束时，Presenter也清除IView对象，不在持有
     */
    @Override
    public void detachView() {
        if (MvpRef != null) {
            MvpRef.clear();
            MvpRef = null;
        }
    }
}

===================================demo========================================
接口：
/**
 * 创建一个类作为纽带，将view、presenter、model的接口方法都串联在一起，更加便于管理
 */
public final class MainContacts {
    public interface IMain extends IView {
        void showTips(boolean isSucceess);
    }

    public interface IMainPre extends IPresenter {
        void login(String username, String password);
    }

    public interface IMainLgc {
        boolean login(String username, String password);
    }
}


Model部分：

public class MainLogic implements MainContacts.IMainLgc {

    public boolean login(String username, String password) {
        if (TextUtils.isEmpty(username) || TextUtils.isEmpty(password)) {
            return false;
        }
        return true;
    }
}


View部分：
public class MainActivity extends BaseActivity<MainPresnter> implements MainContacts.IMain {
    private EditText editT_username, editT_password;
    private Button btn_login;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        initUI();
        addListeners();
    }

    @Override
    protected MainPresnter bindPresenter() {
        return new MainPresnter(this);
    }

    private void initUI() {
        editT_username = $(R.id.editT_username);
        editT_password = $(R.id.editT_password);
        btn_login = $(R.id.btn_login);
    }

    private void addListeners() {
        btn_login.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                MvpPre.login(editT_username.getText().toString(), editT_password.getText().toString());
            }
        });
    }

    @Override
    public void showTips(boolean isSucceess) {
        if (isSucceess) {
            Toast.makeText(this, "登录成功！", Toast.LENGTH_SHORT).show();
        } else {
            Toast.makeText(this, "登录失败！", Toast.LENGTH_SHORT).show();
        }
    }
}


Presenter部分：
public class MainPresnter extends BasePresenter<MainContacts.IMain> implements MainContacts.IMainPre {
    private MainLogic mMainLogic;

    public MainPresnter(MainContacts.IMain view) {
        super(view);
        this.mMainLogic = new MainLogic();
    }

    @Override
    public void login(String username, String password) {
        // 判断activity的生命周期是否结束，不判断的话在极端情况下可能会出现内存泄露
        if (isViewAttach()) {
            MvpRef.get().showTips(mMainLogic.login(username, password));
        }
    }
}


```
> 以上就是我自己对MVP模式的一些理解，如果你不想自己重新搭建MVP模式

可以直接使用MVPLoader项目(这是别人封装好的项目)做依赖：

```java
Step 1:

      allprojects {
          repositories {
              ...
              maven { url 'https://jitpack.io' }
          }
      }

Step 2:

      dependencies {
          compile 'com.github.albert-lii:MVPLoader:1.0.6'
      }
```

### 最后，分析一下其模式的优缺点

 优点：

1.单一职责，Model， View， Presenter只处理单一逻辑

2.解耦：Model层的修改和View层的修改互不影响

3.面向接口编程，依赖抽象：Presenter和View相互持有抽象引用，
对外影藏内部实现细节

缺点：

1.Model进行异步操作的时候，获取结果通过Presenter会传到View的
时候，出现View引用的空指针异常

2.Presenter和View相互持有抽象引用,解除不及时的话容易出现内存泄露
