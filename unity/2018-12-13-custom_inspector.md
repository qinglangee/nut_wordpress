# unity 自定义 inspector面板

## 添加一个按钮
首先写一个功能类, 定义点击按钮时调用的函数
```

	using UnityEngine;

	public class ObjectBuilderScript : MonoBehaviour {
	    public GameObject obj;
	    public Vector3 spawnPoint;
	    public void BuildObject()
	    {
	        Instantiate(obj, spawnPoint, Quaternion.identity);
	    }
	}
```
然后是一个自定义inspector面板的类，这两个类放在项目里就可以了，unity 会自动识别. 当物体上挂载了 ObjectBuilderScript 组件时，Inspector 面板上就会为它添加一个 Build Object 按钮，点击就调用对应的函数。
```

	using UnityEngine;
	using UnityEditor;

	[CustomEditor(typeof(ObjectBuilderScript))]
	public class ObjectBuilderEditor : Editor {
		public override void OnInspectorGUI()
	    {
	        DrawDefaultInspector();
	        ObjectBuilderScript myScript = (ObjectBuilderScript)target;
	        if(GUILayout.Button("Build Object"))
	        {
	            myScript.BuildObject();
	        }
	    }
	}
```


## Unity中的插件机制
Unity有两类插件: Managed plugins和Native plugin。

Managed plugins是托管式.NET代码，因为只有.NET代码，也就是说不能使用.NET库不支持的功能。

Native plugins是平台专门的原生代码库，可以用来访问操作系统调用或者第三方的库。

在Unity5之前，通过插件存放的目录来区分支持的目标平台；然而Unity5可以把插件放在任何目录，通过Plugin Inspector设置相关属性就可以了，但为了兼容以前的版本，Unity5也会支持插件存放的目录，进行默认的插件设置。

规则如下:

文件夹 	                                    默认插件设置
Assets/**/Editor 	                        只兼容Editor
Assets/**/Editor/(x86 or x86_64 or x64) 	只兼容Editor，如果子文件夹存在，用于匹配目标CPU
Assets/Plugins/x86_64(or x64) 	            x64兼容
Assets/Plugins/x86 	                        x86兼容
Assets/Plugins/Android/(x86 or armeabi or armeabi-v7a) 	只跟Android兼容，如果子文件夹存在，用于匹配目标CPU
Assets/Plugins/iOS 	                       只跟iOS兼容


refs:  
[Adding Buttons to a Custom Inspector](https://unity3d.com/cn/learn/tutorials/topics/interface-essentials/adding-buttons-custom-inspector)  
[unity3D 在inspector面板上添加各种控件，国外很好的文章](https://blog.csdn.net/xiaomuzi0802/article/details/41682385)  
[unity3D 插件plugins](https://blog.csdn.net/u014761712/article/details/50604865)  