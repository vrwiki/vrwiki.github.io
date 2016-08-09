# PoolManager使用心得

## 从创建开始

### 1.在Unity场景中的一个物体上,添加Spawn组件.

### 2.其中"Pool Name",是这个对象池的名字,在以后调用的时候要用到.

### 3.创建好了以后,就可以使用这个对象池了

### 4.如果想使用对象池生产一个对象的话,在代码中使用
```
Transform myInstance = PoolManager.Pools["Shapes"].Spawn(myPrefab.transform);
```
这里的"Shapes",就是你所创建的对象池中的"Pool Name",这计划的作用等同于
```
GameObject myInstance = Instantiate(myPrefab);
```
同理,想要销毁对象的话可以这样做
```
PoolManager.Pools["Shapes"].Despawn(myInstance);
```
等同于
```
Destroy(myInstance);
```

### 5.需要注意的是,这些对象中使用的脚本中包含Awake,Start的,如果需要完全模拟,那么应该写相对应的方法
```
public void OnSpawned()
{
  //这里相当于Awake()
}
public void OnDespawned()
{
  //这里相当与Start()
}
```

### 6.还有一些其他选项
#### Match Pool Scale
When an instance is initially created, it will be scaled relative to the Spawn Pool's GameObject. This is great for sprite-based GUI systems, such as nGUI, which often uses a small scale.
#### Match Pool Layer
When an instance is initially created, it's layer will be set to match Spawn Pool's GameObject.
#### Don't Destroy On Load
Activates Unity's DontDestroyOnLoad behavior so the SpawnPool's GameObject is persistent. See the Unity documentation for more information.
#### Log Messages Option
Even if you use PoolManager exclusively through scripting, Log Messages may come in handy during development. Turn this on and start the game to see what PoolManager is doing (Messages are shown in the Unity Console). You can also set this on and off during game-play using PoolManager.LogMessages.
