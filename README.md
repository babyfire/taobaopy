#简介

这是淘宝API的一个简单灵活的Python客户端

##如何使用

	# 引入该Client
	from taobao import APIClient

	client = APIClient('Your API Key','Your API Secret')
	client.items_get(nicks='kamozi', fields='num_iid,title,price', page_no=1, page_size=2)

对于淘宝的某个API,比如 taobao.AA.BB.CC.DD 调用的函数名为 AA_BB_CC_DD，即将前面的taobao.去掉 后面的.全部换成 '_' 

对于get请求 client.get.AA_BB_CC_DD中 get可以省略 即 client.AA_BB_CC_DD

对于post请求 请使用 client.post.AA_BB_CC_DD

如果要上传文件，请使用 client.upload.AA_BB_CC_DD(image=open("Your File Path"))

##例子
####使用POST

	client = APIClient('Your API Key','Your API Secret')
	client.post.items_get(nicks='kamozi', fields='num_iid,title,price', page_no=1, page_size=2)


####访问需授权内容

	client = APIClient('Your API Key','Your API Secret')
	client.post.item_update(num_iid=NUM_IID,title="这是一个新的商品信息服务",session='Your Session Key')


#####或者

	client = APIClient('Your API Key','Your API Secret')
	client.set_token('Your Session Key')
	client.post.item_update(num_iid=NUM_IID,title="这是一个新的商品信息服务")

####上传图片

	client = APIClient('Your API Key','Your API Secret')
	client.set_token('Your Session Key')
	client.upload.item_img_upload(num_iid=NUM_IID, is_major='true', image=open("logo.png","rb"))


####自定义客户端

	def _debug_fetcher(request):
	    opener = urllib2.build_opener(urllib2.HTTPHandler(debuglevel=1))
	    return opener.open(request,timeout=5).read()
	
	client = APIClient('Your API Key','Your API Secret')
	client.set_fetcher(_debug_fetcher)
	client.set_access_token(token)
	client.upload.item_img_upload(num_iid=NUM_IID,is_major='true',image=open("logo.png","rb"))

####访问沙箱

	client = APIClient('Your API Key','Your API Secret',domain='container.api.tbsandbox.com')
	client.items_get(nicks='test',fields='num_iid,title,price',page_no=1,page_size=2)

