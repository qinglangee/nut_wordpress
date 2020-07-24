# json 解析
使用 Newtonsoft.Json   https://github.com/JamesNK/Newtonsoft.Json

主要就这两个方法  
*Unity中使用.NET35的版本，更高的版本Unity可能还不支持*
```

	string output = JsonConvert.SerializeObject(product);
	//{
	//  "Name": "Apple",
	//  "ExpiryDate": "2008-12-28T00:00:00",
	//  "Price": 3.99,
	//  "Sizes": [
	//    "Small",
	//    "Medium",
	//    "Large"
	//  ]
	//}

	Product deserializedProduct = JsonConvert.DeserializeObject<Product>(output);
```


[这篇文章][1]讲得比较多方法   

refs:  
[C#解析json文件的方法][1]  


[1]: http://www.cnblogs.com/txw1958/archive/2012/08/01/csharp-json.html