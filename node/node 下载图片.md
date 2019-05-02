# node 下载图片

基于 http/https 模块请求数据，再用流处理到具体文件。

``` js
const img_url = 'https://www.eefung.com/image/62d9b892-432f-4db0-acf0-6997f534c8c4';

var https = require('https'),                                                
    Stream = require('stream').Transform,         
    path = require('path'),                         
    fs = require('fs');                                                                        

https.request(
  img_url,
  {
    headers: {
      'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.103 Safari/537.36',
      cookie: 'UM_distinctid=167012ff04cd2-018f9f3080bfe8-4313362-144000-167012ff04e4c6; _qddaz=QD.3hqo3i.ygezzq.jocfan7g; pgv_pvi=4443619328; tencentSig=4363339776; __root_domain_v=.eefung.com; 3b1aecabfa301267aca507a252c2b25b=98613dfded4480336a3add2219d70d47; Hm_lvt_eea265e0f0313c48f026fa00f18c6908=1555577711,1555912653,1556693440,1556712357; CNZZDATA2970921=cnzz_eid%3D1869345497-1541910468-%26ntime%3D1556715288; _pk_ref.8.6e87=%5B%22%22%2C%22%22%2C1556719123%2C%22http%3A%2F%2Fjuhuadata.com%2Fyuqing%22%5D; _pk_id.8.6e87=ef3ef4232b2b74ef.1541913178.43.1556720481.1556719123.; Hm_lpvt_eea265e0f0313c48f026fa00f18c6908=1556720481',
      Host: 'www.eefung.com'
    }
  }, 
  function(response) {                                        
    var data = new Stream();                                                    

    response.on('data', function(chunk) {                                       
      data.push(chunk);                                                         
    });                                                                         

    response.on('end', function() {                                             
      fs.writeFileSync(path.resolve(__dirname, 'img_download.png'), data.read());                               
    });                                                                         
  }
).end();
```
