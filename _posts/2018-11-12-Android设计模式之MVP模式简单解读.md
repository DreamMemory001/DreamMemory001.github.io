---
layout:     post
title:      Android���ģʽ
subtitle:   MVPģʽ�򵥽��
date:       2018-11-12
author:     TkiChus
header-img: img/post-bg-mvp.jpg
catalog: true
tags:
    - TkiChus
    - DreamMemory001 Blog
    - Android
---
# MVPģʽ�򵥽���

     ��Android�Ŀ����У�����ͨ���Ὣһ����Ŀ�ֳ�һ������ģ���ļ��������й���ά����
     �е�����ֱ�Ӱ��չ�������ģ�飬��Ҳ����������ģʽ�������е�����ᰴ��һ��
    ���ģʽ���ٽ�Ϲ�����������Ŀģʽ����ƣ��������ڳ���MVP��MVVM������Ŀǰ�Ƚ�
    ���е���Ŀ���ģʽ�������ͽ��ܵ���MVPģʽ��


### MVPģʽ����MVCģʽ���ݻ������ġ��������Ƚ���һ�¶Ա�

> MVC

M��model��ģ��, ��Ӧ�ó��������ڴ���Ӧ�������߼��Ĳ��֣�
ͨ��ģ�Ͷ����������ݿ��н��д�ȡ

V(view)��ͼ�� ��Ӧ�ó����д������ݵ���ʾ���֣�ͨ����ͼ
��һ��ģ��������������

C��controller���������� ��Ӧ�ó����д����û������Ĳ��֣�
ͨ���������������ͼ��ȡ���ݣ������û������룬����ģ�ͷ���
���ݡ�

> MVP

MVP

M��model���������ݵ����󣬽��������˵����ݲ���

V��View������ͼʾ����չʾ��ͼʾ�¼�����Activity��
Fragment��Dialog��ViewGroup�ȳ�����ͼ����������Գе���
��ɫ

P��presenter����View��Model����������

* MVPģʽ��MVCģʽ�Ա�ͼ

![](http://ww1.sinaimg.cn/large/006nBCHPly1fzsdttxqkcj30lm099t9l.jpg)

### ʹ��MVP��ԭ��

��Android�У�����Activity��û����ȷ��˵��������
View����Controller�ķ��룬Activity����View������
��Ҳ����Controller�����ʣ����Ե���MVC��Android�к�
����ȷ�ֹ�ʹ�ã�����Activity���ء�����MVC�е�View��
��Modelֱ�ӽ���������Activity��Model������Ժܸߣ���
����ά��ʱ�����б䶯������Model��Activity��XML�����
�Ÿı䣬�������ܴ󣬳ɱ�̫�ߡ�

��MVP��MVC���Ĳ�֮ͬ����MVP��M��V�ָ�����ͨ��P������
������Android�У��Ϳ�����ȷ�İ�Activity����View����
��Ȼ���ܻ���һ���߼������У������Ѿ����˴��ţ�View��Model
��ֱ�ӽ�������View�б䶯����Model�б䶯ʱ�������໥Ӱ��
����̫��䶯������Եͣ����ں���ά����˵���ر�����ĿԽ��Խ�Ӵ�
ʱ�����Ժܿ��������Ŀ�Ľṹ���ҵ���Ҫ�޸ĵĵط����������
�˹����������ң� ��ΪView��Model�����Ե�ʣ�Model���Ե���
���е�Ԫ���ԡ�

���ԣ���������Ϊ��������ĿԽ��Խ�Ӵ󣬲�������MVP+DataBing
����ʵ����е�������MVPģʽ�������ݣ���ʹ��Ŀ�Ӵ󣬸ı�ʱҲ
����Ҫ̫���ع���


### MVPLoader

> �������Լ�д�Ĵ���

```java
==================================View=======================================

���е�view��Activity��FragmentActivity��Fragment...��������ʵ������ӿ�

public interface IView {
    // �˷�����Ϊ�˵�Presenter����Ҫ��ȡ�����Ķ���ʱ�����������Ķ��󣬶�������Presenterֱ�ӳ�������  �Ķ���
    Activity getSelfActivity();
}

����Activity�Ļ��ࣺ

public abstract class BaseActivity<P extends IPresenter> extends Activity implements IView {
    // Presenter����
    protected P MvpPre;

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        MvpPre = bindPresenter();
    }

    // ��Presenter
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
         * ���������ڽ���ʱ����presenter��view֮�����ϵ�Ͽ�����ֹ�����ڴ�й¶
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

Presenter�Ļ��ࣺ

public abstract class BasePresenter<V extends IView> implements IPresenter {
    // �˴�ʹ������������Ϊ����ʱActivity�رղ�һ������onDestroy��������ʱʹ�������ÿ��Լ�ʱ����IView
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
     * ��Ҫ�����ж�IView�����������Ƿ��������ֹ�����ڴ�й¶״��
     *
     * @return
     */
    protected boolean isViewAttach() {
        return MvpRef != null && MvpRef.get() != null;
    }

    /**
     * Activity�������ڽ���ʱ��PresenterҲ���IView���󣬲��ڳ���
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
�ӿڣ�
/**
 * ����һ������ΪŦ������view��presenter��model�Ľӿڷ�����������һ�𣬸��ӱ��ڹ���
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


Model���֣�

public class MainLogic implements MainContacts.IMainLgc {

    public boolean login(String username, String password) {
        if (TextUtils.isEmpty(username) || TextUtils.isEmpty(password)) {
            return false;
        }
        return true;
    }
}


View���֣�
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
            Toast.makeText(this, "��¼�ɹ���", Toast.LENGTH_SHORT).show();
        } else {
            Toast.makeText(this, "��¼ʧ�ܣ�", Toast.LENGTH_SHORT).show();
        }
    }
}


Presenter���֣�
public class MainPresnter extends BasePresenter<MainContacts.IMain> implements MainContacts.IMainPre {
    private MainLogic mMainLogic;

    public MainPresnter(MainContacts.IMain view) {
        super(view);
        this.mMainLogic = new MainLogic();
    }

    @Override
    public void login(String username, String password) {
        // �ж�activity�����������Ƿ���������жϵĻ��ڼ�������¿��ܻ�����ڴ�й¶
        if (isViewAttach()) {
            MvpRef.get().showTips(mMainLogic.login(username, password));
        }
    }
}


```
> ���Ͼ������Լ���MVPģʽ��һЩ��⣬����㲻���Լ����´MVPģʽ

����ֱ��ʹ��MVPLoader��Ŀ(���Ǳ��˷�װ�õ���Ŀ)��������

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

### ��󣬷���һ����ģʽ����ȱ��

 �ŵ㣺

1.��һְ��Model�� View�� Presenterֻ����һ�߼�

2.���Model����޸ĺ�View����޸Ļ���Ӱ��

3.����ӿڱ�̣���������Presenter��View�໥���г������ã�
����Ӱ���ڲ�ʵ��ϸ��

ȱ�㣺

1.Model�����첽������ʱ�򣬻�ȡ���ͨ��Presenter�ᴫ��View��
ʱ�򣬳���View���õĿ�ָ���쳣

2.Presenter��View�໥���г�������,�������ʱ�Ļ����׳����ڴ�й¶
