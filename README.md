# HuobiWs
火币websocket接口java封装.
修改
WsMain:
    String url = "wss://api.huobi.br.com/ws";
		WebSoketClient client = new WebSoketClient(url, service);
		client.start();
		client.addSub("market.btcusdt.kline.1min", "client1");
    
WebSocketService:
    public void onReceive(JSONObject json) {
		//log.info("receive:" + json.toJSONString());
		try {
			if (json.toJSONString().length()>50){
				String ts= json.getString("ts");
				String tick= json.getString("tick");
				JSONObject json2=JSONObject.parseObject(tick);
				String close=json2.getString("close");
				Date date = new Date(Long.valueOf(ts));
				SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
				log.info("时间:"+format.format(date)+","+"最新价:"+close.substring(0,8));
			}else{
				log.info("receive:" + json.toJSONString());
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
