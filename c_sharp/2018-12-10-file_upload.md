# c# 上传文件


```

	using System;
	using System.Collections.Generic;
	using System.Text;
	using System.Net;
	using System.IO;
	using System.Collections.Specialized;

	namespace up
	{
	    class Upload
	    {
	        static void Main(string[] args)
	        {
	            String url = "http://192.168.3.18:6024/game/pic/save";
	            String path = "D:\\temp\\d3\\up.jpeg";
	            String content = UploadFile(url, path);
	            Console.WriteLine(content);
	        }


	        /// <summary>
	        /// Http上传文件
	        /// </summary>
	        public static string UploadFile(string url, string path)
	        {
	            // 设置参数
	            HttpWebRequest request = WebRequest.Create(url) as HttpWebRequest;
	            CookieContainer cookieContainer = new CookieContainer();
	            request.CookieContainer = cookieContainer;
	            request.AllowAutoRedirect = true;
	            request.Method = "POST";
	            string boundary = DateTime.Now.Ticks.ToString("X"); // 随机分隔线
	            request.ContentType = "multipart/form-data;charset=utf-8;boundary=" + boundary;
	            byte[] itemBoundaryBytes = Encoding.UTF8.GetBytes("\r\n--" + boundary + "\r\n");
	            byte[] endBoundaryBytes = Encoding.UTF8.GetBytes("\r\n--" + boundary + "--\r\n");

	            int pos = path.LastIndexOf("\\");
	            string fileName = path.Substring(pos + 1);


	            string paramTemplate = "\r\n--" + boundary + "\r\nContent-Disposition: form-data; name=\"{0}\";\r\n\r\n{1}";

	            //请求头部信息
	            StringBuilder sbHeader = new StringBuilder(string.Format("Content-Disposition:form-data;name=\"upload\";filename=\"{0}\"\r\nContent-Type:application/octet-stream\r\n\r\n", fileName));
	            byte[] postHeaderBytes = Encoding.UTF8.GetBytes(sbHeader.ToString());

	            FileStream fs = new FileStream(path, FileMode.Open, FileAccess.Read);
	            byte[] bArr = new byte[fs.Length];
	            fs.Read(bArr, 0, bArr.Length);
	            fs.Close();

	            Stream postStream = request.GetRequestStream();

	            byte[] paramBytes = Encoding.UTF8.GetBytes(string.Format(paramTemplate, "pass", "123456"));
	            postStream.Write(paramBytes, 0, paramBytes.Length);
	            paramBytes = Encoding.UTF8.GetBytes(string.Format(paramTemplate, "username", "balabala"));
	            postStream.Write(paramBytes, 0, paramBytes.Length);

	            postStream.Write(itemBoundaryBytes, 0, itemBoundaryBytes.Length);
	            postStream.Write(postHeaderBytes, 0, postHeaderBytes.Length);
	            postStream.Write(bArr, 0, bArr.Length);
	            postStream.Write(endBoundaryBytes, 0, endBoundaryBytes.Length);
	            postStream.Close();

	            //发送请求并获取相应回应数据
	            HttpWebResponse response = request.GetResponse() as HttpWebResponse;
	            //直到request.GetResponse()程序才开始向目标网页发送Post请求
	            Stream instream = response.GetResponseStream();
	            StreamReader sr = new StreamReader(instream, Encoding.UTF8);
	            //返回结果网页（html）代码
	            string content = sr.ReadToEnd();
	            return content;
	        }
	    }
	}
```