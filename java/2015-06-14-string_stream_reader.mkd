# String Reader Stream 转换

##　1、String –> InputStream

	InputStrem is = new ByteArrayInputStream(str.getBytes());
or

	ByteArrayInputStream stream
	= new ByteArrayInputStream(str.getBytes());


##　2、InputStream–>String


	inputStream input;

	StringBuffer out = new StringBuffer();
	     byte[] b = new byte[4096];
	     for (int n; (n = input.read(b)) != -1;) {
	      out.append(new String(b, 0, n));
	     }
	out.toString();
##　3、Reader –>String

	BufferedReader in = new BufferedReader(new InputStreamReader(is));
	StringBuffer buffer = new StringBuffer();
	String line = " ";
	while ((line = in.readLine()) != null){
	buffer.append(line);
	}
	return buffer.toString();


##　4、String–>Reader

	Reader reader = null;
	BufferedReader r = new BufferedReader(reader);
	StringBuilder b = new StringBuilder();
	String line;
	while((line=r.readLine())!=null) {
	b.append(line);
	b.append(“\r\n”);
	}
	b.toString();

from http://ruixiazun.blog.163.com/blog/static/90687918201011231076542/

refs:  


[String Reader Stream 之间的转换](http://www.cnblogs.com/clarkchen/archive/2011/03/09/1978570.html)  