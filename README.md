#       YKS开放第三方平台sku与订单接口文档v0.1  
  
### 1. 获取SKU详情
**接口地址**： sku.detail.get  
**请求方式**： POST  
**参数校验**： 暂无  
**接口描述**： 通过单个SKU ID获取YKS SKU 详情信息  
**Auth-date**：[add by jiangshilin 2017-8-02] 
#####   请求格式：  
```json 
{
"sku":"A301"//YKS-SKU（必填）
}//请求对象
```  
  
#####   返回格式：  
```json  
{
    "sku": "A301",
    "spu": "5238",
    "cnname": "20g秤0.001G",
    "enname": "0.001g/20g Digital LCD Balance Weight Milligram Pocket Jewelry Diamond Scale",
    "status": "1",//sku状态 1 正常销售 2 清库存 3 缺货 4 下架 5 清库存（侵权/违禁） 6 包材 7 正常（配件） 8 菜鸟模型产品 9 海外仓 10 亚马逊 11 下架（侵权/违禁）
    "category_1": "家装/灯具",//一级分类名
    "category_2": "五金工具",//二级分类名
    "category_3": "电子称",//三级分类名
    "cateId":123,//三级分类id
    "logic_attr": "101",//sku物流属性
    "weight": "228.0000",//重量(g)
    "price": "55.0000",//成本价
    "length": "150.0000",//长(mm)
    "width": "40.0000",//宽(mm)
    "height": "140.0000",//高(mm)
    "asweight": "238.0000",//包装后重量(g)
    "aslength": "210.0000",//包装后长(mm)
    "aswidth": "200.0000",//包装后宽(mm)
    "asheight": "70.0000",//包装后高(mm)
    "is_multiplicity": null,
    "color": "black&silvery",//颜色
    "size": "",//尺寸
    "type": "",//类型
    "stock":100,//库存
    "attr_value": {
        "Maximum Weight Recommendation": "20",
        "Health Scale Weight Indication": "Digital(数字)",
        "Health Scale Metal Bonding Point": "Digital(数字)",
        "Model Number": "A301",
    },//sku属性
    "desc_main": {
        "en": "<strong>Search term:</strong><br/>0.001g/20g, Mini Size, Digital LCD Screen, <span style=\"color: rgb(255, 0, 0);\">Milligram Pocket Scale</span>, Jewelry Scale, Diamond Scale<br/><br/><strong>Features:</strong><br/>6 different weighing modes.<br/>",//sku英文详情
        "fr": "",
        "ru": "",
		....
    },//sku描述详情
    "unplatsite": "",//禁用平台
    "img":{
		"C": {
			"1": "https://img2.photo137.com/MOBILE/A301-C-1-114.jpg"
		},
		"D": {
			"2": "https://img2.photo137.com/MOBILE/A301-D-2-114.jpg",
			"3": "https://img2.photo137.com/MOBILE/A301-D-3-114.jpg",
			"4": "https://img2.photo137.com/MOBILE/A301-D-4-114.jpg",
			"5": "https://img2.photo137.com/MOBILE/A301-D-5-114.jpg",
			"6": "https://img2.photo137.com/MOBILE/A301-D-6-114.jpg",
			"7": "https://img2.photo137.com/MOBILE/A301-D-7-114.jpg",
			"8": "https://img2.photo137.com/MOBILE/A301-D-8-114.jpg"
		}
	}//sku图片详情
} 
  
```  
#####   错误返回：  
```json  
{
    "status": 400,
    "msg": "A3012该sku不存在或是已被禁用",
}  

```
***  
### 2.获取SKU库存接口  
**接口地址**： sku.stock.get  
**请求方式**： POST  
**参数校验**： 暂无  
**接口描述**： 通过SKU 获取YKS SKU 库存信息 （最多一次返回1000个）  
**Auth-date**：[add by jiangshilin 2017-8-02] 
#####   请求格式：  
```json  
["A301","ZG638001"] //skulist(必填)
```
####    返回格式
```json
{
	"status": 0,
	"msg": "全部成功",
	"successData": [{
		"sku": "A301",
		"stock": "100"
	}],
	[{
		"sku": "ZG638001",
		"stock": "50"
	}]
}

```  
####    错误返回

```json
{
	"status": 400,
	"msg": "找不到所有sku库存信息",
}

{
	"status": 3,
	"msg": "返回部分sku库存信息",
	"successData": [{
		"sku": "A301",
		"stock": "100"
	}],//成功sku
	"failData":["ZG638001"] //失败sku
}

```  
***
### 3.新增订单接口  
**接口地址**： order.add  
**请求方式**： POST  
**参数校验**： 暂无  
**接口描述**： 通过用户提交第三方订单及商品信息生成暂存订单（暂存时间待定，定时推送到erp系统生成订单） （最多一次生成500个）  
**Auth-date**：[add by jiangshilin 2017-8-02] 
#####   请求格式：  
```json  
[{
    "order_sn": "2017080288888",//第三方订单号（必填）
    "remark": "订单备注",
    "create_time": "创建时间",
    "buyer_id": "收货用户信息",
    "buyer_city": "收货城市",
    "buyer_address": "收货详细地址",
    "bb_type": "ZY01（用户类型）",
    "skus": [
        {
            "sku": "A301",//YKS-sku （必填）
            "third_sku": "66666",//第三方sku (必填)
            "third_item": "9999",//第三方商品id
            "sku_count": 6,//sku数量
            "sku_price": "6.6",//sku价格
            "warehouseid": 1,//仓库
            "products_place": 6666//储位
        },
        {
            "sku": "A302",
            "third_sku": "66662",
            "third_item": "9999",
            "sku_count": 6,
            "sku_price": "6.7",
            "warehouseid": 1,
            "products_place": 6666
        }
    ]
}]
```
####    返回格式
```json
{
	"status":0,
	"msg":"新增成功"
}
```  
####    错误返回

```json
{
	"status": 400,
	"msg": "找不到所有sku信息",
}

{
	"status": 3,
	"msg": "部分订单号已经存在",
	"successData":["2017080299999"],//成功订单
	"failData":["2017080266666"] //失败订单
}

```  
***

### 4.修改订单接口  
**接口地址**： order.edit  
**请求方式**： POST  
**参数校验**： 暂无  
**接口描述**： 通过用户提交第三方订单及商品信息更新还未推送erp的订单 （最多一次编辑500个）  
**Auth-date**：[add by jiangshilin 2017-8-02] 
#####   请求格式：  
```json  
[{
    "order_sn": "2017080288888",//第三方订单号
    "remark": "订单备注",
    "create_time": "创建时间",
    "buyer_id": "收货用户信息",
    "buyer_city": "收货城市",
    "buyer_address": "收货详细地址",
    "bb_type": "ZY01（用户类型）",
    "skus": [
        {
            "sku": "A301",//YKS-sku
            "third_sku": "66666",//第三方sku
            "third_item": "9999",//第三方商品id
            "sku_count": 6,//sku数量
            "sku_price": "6.6",//sku价格
            "warehouseid": 1,//仓库
            "products_place": 6666//储位
        },
        {
            "sku": "A302",
            "third_sku": "66662",
            "third_item": "9999",
            "sku_count": 6,
            "sku_price": "6.7",
            "warehouseid": 1,
            "products_place": 6666
        }
    ]
}]
```
####    返回格式
```json
{
	"status": 0,
	"msg": "编辑成功"
}//新增成功提示

```  
####    错误返回

```json
{
	"status": 400,
	"msg": "找不到所有sku信息",
}

{
	"status": 4,
	"msg": "部分订单号已经在erp生成不允许编辑",
	"successData":["2017080299999"],//成功订单
	"failData":["2017080266666"] //失败订单
}

```  
***

### 5.获取订单详情接口  
**接口地址**： order.detail.get  
**请求方式**： POST  
**参数校验**： 暂无  
**接口描述**： 通过单个第三方订单获取订单详情   
**Auth-date**：[add by jiangshilin 2017-8-02] 
#####   请求格式：  
```json  
{
"order_sn":"2017080299999",//第三方订单号（与erp_order_sn二选一或者都填写）
"erp_order_sn":"13434322343"//YKS erp订单号（与order_sn二选一或者都填写）
}//请求对象
```
####    返回格式
```json
{
    "order_sn": "2017080288888",
    "remark": "订单备注",
    "create_time": "创建时间",
    "buyer_id": "收货用户信息",
    "buyer_city": "收货城市",
    "buyer_address": "收货详细地址",
    "bb_type": "ZY01（用户类型）",
    "status": "1",//当前订单状态 0，未推送erp；1，已生成erp订单；-1，erp，订单生成失败
    "error_log":"失败日志",
    "erp_order_sn": "13434322343",
    "logistics_proce":"物流渠道"，
    "logistics_no":"追踪号",
    "logistics_freight":"物流运费",
    "merchant_remark": "商家备注",
    "skus": [
        {
            "sku": "A301",
            "third_sku": "66666",
            "third_item": "9999",
            "sku_count": 6,
            "sku_price": "6.6",
            "warehouseid": 1,
            "products_place": 6666
        },
        {
            "sku": "A302",
            "third_sku": "66662",
            "third_item": "9999",
            "sku_count": 6,
            "sku_price": "6.7",
            "warehouseid": 1,
            "products_place": 6666
        }
    ]
}

```  
####    错误返回

```json
{
	"status": 400,
	"msg": "找不到商家订单信息",
}//找不到订单提示信息


```  
***

### 6.分页获取sku列表接口  
**接口地址**： sku.list.get  
**请求方式**： POST  
**参数校验**： 暂无  
**接口描述**： 通过分页参数获取sku列表  
**Auth-date**：[add by jiangshilin 2017-8-02] 
#####   请求格式：  
```json  
{
"page":"1",//当前页（默认1）
"limit":"100",//每页数量(默认100，最大200)
"cateId":"100"//分类id（非必填 默认0，返回所有）
}//请求对象
```
####    返回格式
```json
{
    "status": 0,
    "pagination": {
        "page": 1,//数据当前页
        "limit": 200,//数据每页条数
        "total": "1000",//数据总条数
    },
    "data": [
        {
            "sku": "BR409",
            "cnname": "TITANB3",
            "enname": "7.4v 11.1v Li-polymer Battery Charger 2s 3s Cells for RC LiPo AEG Airsoft batter",
            "stock": "300",
            "status": 1
        },
        {
            "sku": "A301",
            "cnname": "20g秤0.001G",
            "enname": "0.001g/20g Digital LCD Balance Weight Milligram Pocket Jewelry Diamond Scale",
            "stock": "300",//库存
            "status": 1,//1 正常销售 2 清库存 3 缺货 4 下架 5 清库存（侵权/违禁） 6 包材 7 正常（配件） 8 菜鸟模型产品 9 海外仓 10 亚马逊 11 下架（侵权/违禁）
        }
    ]
}

```  
####    错误返回

```json
{
	"status": 400,
	"msg": "数据为空",
}//找不到sku列表数据提示信息


```  
***

### 7.通过更新时间分页获取sku库存列表接口 
**接口地址**： sku.list.stock.get  
**请求方式**： POST  
**参数校验**： 暂无  
**接口描述**： 通过时间及分页参数获取sku库存列表  
**Auth-date**：[add by jiangshilin 2017-8-02] 
#####   请求格式：  
```json  
{
"page":"1",//当前页（默认1）
"limit":"100",//每页数量(默认100，最大200)
"update_start":"2017-07-08 10:10:10",//库存变更开始时间
"update_end":"2017-08-02 10:10:10",//库存变更结束时间(默认当前时间)
}//请求对象
```
####    返回格式
```json
{
    "status": 0,
    "pagination": {
        "page": 1,//数据当前页
        "limit": 200,//数据每页条数
        "total": "1000",//数据总条数
    },
    "data": [
        {
            "sku": "BR409",
            "stock": "300",
        },
        {
            "sku": "A301",
            "stock": "300",//库存
        }
    ]
}

```  
####    错误返回

```json
{
	"status": 400,
	"msg": "数据为空",
}//找不到sku库存列表数据提示信息


```  
***

### 8.YKS分类列表接口  
**接口地址**： category.list.get  
**请求方式**： POST  
**参数校验**： 暂无  
**接口描述**： 获取YKS所有分类列表  
**Auth-date**：[add by jiangshilin 2017-8-02] 
#####   请求格式：  
```json  
无参数
```
####    返回格式
```json
[
    {
        "cateId": 2,
        "cateNameCn": "女装",
        "subCategorys": [
            {
                "cateId": 3,
                "cateNameCn": "裤子",
                "subCategorys": [
                    {
                        "cateId": 4,
                        "cateNameCn": "牛仔库",
                        "subCategorys": null
                    }
                ]
            }
        ]
    },
    {
        "cateId": 6,
        "cateNameCn": "男装",
        "subCategorys": [
            {
                "cateId": 7,
                "cateNameCn": "上衣",
                "subCategorys": [
                    {
                        "cateId": 8,
                        "cateNameCn": "卫衣",
                        "subCategorys": null
                    }
                ]
            }
        ]
    }
]

```  
####    错误返回

```json
{
	"status": 400,
	"msg": "数据为空",
}//找不到数据信息


```  
***

### 9.分页获取SPU及对应sku列表接口  
**接口地址**： spu.sku.list.get  
**请求方式**： POST  
**参数校验**： 暂无  
**接口描述**： 通过分页参数获取SPU及对应sku列表  
**Auth-date**：[add by jiangshilin 2017-8-09] 
#####   请求格式：  
```json  
{
"page":"1",//当前页（默认1）
"limit":"100",//每页数量(默认100，最大200)
"cateId":"100"//分类id（非必填 默认0，返回所有）
}//请求对象
```
####    返回格式
```json
{
    "status": 0,
    "pagination": {
        "page": 1,
        "limit": 1,
        "total": "50406"
    },
    "data": {
        "1": [//spuid
            {
                "sku": "AS350",
                "cnname": "钻石纹身袜",
                "enname": "Women's Sexy Sheer Transparent Tattoo Pantyhose",
                "stock": "2"
            }
        ]
    }
}

```  
####    错误返回

```json
{
	"status": 400,
	"msg": "数据为空",
}//找不到sku列表数据提示信息


```  
***
