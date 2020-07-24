# unity3d 中拖拽物体

## Input.mousePosition
Vector3  x: 屏幕横轴  y: 屏幕纵轴  z: 离摄像机的距离  
Unity中屏幕左下角(0, 0), 右上角 (camera.pixelWidth - 1, camera.pixelHeight - 1)  


## 鼠标拖动物体
```

	// 屏幕与空间坐标的转换
	Vector3 screenPoint;  Vector3 offset;
	obj = gameObject;   mPos = Input.mousePosition;

	void OnMouseDown(){
		// 物体空间坐标转换为屏幕坐标
		screenPoint = Camera.main.WorldToScreenPoint(obj.transform.position);
		// 物体与光标位置的屏幕平面距离
		offset = obj.transform.position - Camera.main.ScreenToWorldPoint(new Vector(mPos.x, mPos.y, screenPoint.z));
	}
	
	void OnMouseDrag(){
		// 拖鼠标物体跟着动
		Vector3 cursorScreenPoint = new Vector3(mPos.x, mPos.y, screenPoint.z);
		Vector3 cursorPosition = Camera.main.ScreenToWorldPoint(cursorScreenPoint) + offset;
		transform.position = cursorPosition;
	}	

```

## 物体移动到鼠标点击位置
```

	void Update(){
	     Vector3 mouse = Input.mousePosition;
	     Ray castPoint = Camera.main.ScreenPointToRay(mouse);
	     RaycastHit hit;
	     if (Physics.Raycast(castPoint, out hit, Mathf.Infinity))
	     {
	         objectToMove.transform.position = hit.point;
	     }
	 }
```




refs:  
[Getting mouse position in unity](https://stackoverflow.com/questions/46998241/getting-mouse-position-in-unity)  
[Drag object Script in Unity3D](https://letsgeekblog.wordpress.com/2017/03/11/drag-object-script-in-unity3d/)  