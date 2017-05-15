# HttpClient 4.3.3 cookie rejected的解决办法
RequestConfig 可以设置 cookie 策略


	RequestConfig oldConfig = getWrapperClient().getProxyConfig();
	RequestConfig requestConfig = null;
	// 英才登录时cookie不标准，会被拒， 设置一个简单点的 cookie 标准
	if (oldConfig == null) {
		requestConfig = RequestConfig.custom().setCookieSpec(CookieSpecs.NETSCAPE).build();
	} else {
		requestConfig = RequestConfig.copy(oldConfig).setCookieSpec(CookieSpecs.NETSCAPE).build();
	}
	HttpPost post = new HttpPost(url);
	// config 设置
	if (getProxyConfig() != null) {
		post.setConfig(requestConfig);
	}
创建一个空的没有验证的策略， 这个方法不太好，啥都不干总学得少点啥

	BasicCookieStore cookieStore = new BasicCookieStore();
	CookieSpecProvider easySpecProvider = new CookieSpecProvider() {
		public CookieSpec create(HttpContext context) {

			return new BrowserCompatSpec() {
				@Override
				public void validate(Cookie cookie, CookieOrigin origin)
				throws MalformedCookieException {
				// Oh, I am easy
				}
			};
		}
	};
	Registry<CookieSpecProvider> r = RegistryBuilder
		.<CookieSpecProvider> create()
		.register(CookieSpecs.BEST_MATCH, new BestMatchSpecFactory())
		.register(CookieSpecs.BROWSER_COMPATIBILITY,
		new BrowserCompatSpecFactory())
		.register("easy", easySpecProvider).build();

	RequestConfig requestConfig = RequestConfig.custom()
		.setCookieSpec("easy").setSocketTimeout(10000)
		.setConnectTimeout(10000).build();

	CloseableHttpClient httpclient = HttpClients.custom()
		.setDefaultCookieSpecRegistry(r)
		.setDefaultRequestConfig(requestConfig)
		.setDefaultCookieStore(cookieStore)
		.build();


refs:  
[HttpClient 4.3.3 cookie rejected的解决办法](http://www.tuicool.com/articles/MZ36Zz)  