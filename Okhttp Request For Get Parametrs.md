## Okhttp Request For Get Parametrs 

 
 ```java
 	//  http request parameters
    
    	// Client
    	OkHttpClient client = new OkHttpClient();
   		//get request
 		HttpUrl.Builder urlBuilder = 
  		  	HttpUrl
				.parse(url)
				.newBuilder()
				.addQueryParameter("example1", "value 1")
				.addQueryParameter("example2", "value 2");

		 // wwww.example.com?example1=value&example2=value2 .....
		String url = urlBuilder.build().toString();
        
        Request request = new Request.Builder()
                .url(url)
                .get()
                .build();
    
        // post request
        MultipartBody.Builder builder = new MultipartBody.Builder();
                    builder.setType(MultipartBody.FORM)
                            .addFormDataPart("example1", "value 1")
							.addFormDataPart("example2", "value 2");;
		RequestBody requestBody = builder.build();
        
		Request request = new Request.Builder()
                    .url(url)
                    .post(requestBody)
                    .build();
                    
                
        // response 
        client.newCall(request).enqueue(new Callback() {
            @Override
            public void onFailure(Call call, IOException e) {
                Toast.makeText(context, getResources().getString(R.string.failed), Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onResponse(Call call, final Response response) throws IOException {
                if (response.isSuccessful()) {
                    JSONObject jsonObject = null;
                    try {
                        Gson gson = new Gson();
                        exampleModel model = gson.fromJson(response.body().string().toString(), exampleModel.class);

                    } catch (JSONException e) {
                        e.printStackTrace();
                    }
                }
            }
        });

    
 ```
 
 ## Webview post Parameters 


```java 
// webview settings
WebView webView = (WebView) findViewById(R.id.web_view);
        webView.getSettings().setDomStorageEnabled(true);
        webView.getSettings().setAllowContentAccess(true);
        webView.getSettings().setAppCacheEnabled(true);
        webView.getSettings().setBlockNetworkImage(false);
        webView.getSettings().setBlockNetworkLoads(false);
        webView.getSettings().setLoadsImagesAutomatically(true);
        webView.getSettings().setJavaScriptEnabled(true);
        webView.getSettings().setJavaScriptCanOpenWindowsAutomatically(true);
        webView.getSettings().setDatabaseEnabled(true);
        webView.getSettings().setAllowFileAccess(true);
        CookieManager.getInstance().setAcceptCookie(true);

	Map<String, String> mapParams = new HashMap<String, String>();
	mapParams.put("param1", value1);
	mapParams.put("param2", value2);
	mapParams.put("param3", value3);
	mapParams.put("param4", value4);
	mapParams.put("param5", value5);

 	StringBuilder sb = new StringBuilder();
 	sb.append("<html>");
 	sb.append("<head></head>");
 	sb.append("<body>");
 	sb.append(String.format("<form id='form1' action='%s' method='%s'>", responseModel.getServerUrl(), "post"));
 		for (Map.Entry<String, String> item : mapParams.entrySet()) {
 		    sb.append(String.format("<input name='%s' type='hidden' value='%s' />", item.getKey(), item.getValue()));
 		}
 	sb.append("</form>");
 	sb.append("<script type=\"text/javascript\">document.getElementById('form1').submit();</script>");
 	sb.append("</body>");
 	sb.append("</html>");
 	String pageContent = sb.toString();

 	webView.post(new Runnable() {
	    public void run() {
	        webView.loadData(pageContent, "text/html", "UTF-8");
	    }
	});

```


