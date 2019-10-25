# 关于API接入
本节将会通过一个示例介绍API的接入流程，也可参考UCloud官方[API 文档综览](https://docs.ucloud.cn/api/summary/overview)。需要JAVA/GO/PHP/Python等语言的参考，可以参考UCloud SDK框架[UCloud SDK项目](https://github.com/ucloud?utf8=%E2%9C%93&q=SDK&type=&language=)。



## API调用示例
本节通过一个具体的示例（获取设备影子）介绍如何实现API调用。用户可将其中的参数换成自己的实际参数进行测试。

0. 概述   
   
   接口的调用使用HTTP GET或POST调用都可以得到相同的结果。调用的参数包括接口的参数+公共参数+参数签名三部分。
   - 接口参数：某个具体接口需要的参数；
   - 公共参数：每个接口都需要用到的，包括调用接口名、项目名、公钥等
   - 签名：通过私钥签名，方便网关鉴权。

1. 查看接口文档获取接口名及参数   

   名称| 内容
   ---|---
   接口名| [GetUIoTCoreDeviceShadow](../api_guide/deviceshadowmgmtapi) - 获取设备影子。
   接口参数|**Region**：上海二区，地域ID为    [cn-sh2](https://docs.ucloud.cn/api/summary/regionlist)。<br>**ProductSN**：产品序列号为    `8pi2i730vxsala2a`，通过控制台查看。<br>**DeviceSN**：设备序列号为`ark1d4ug1evfb1jy`，通过控制台查看。

2. 获取公共参数，即每次请求都需要的参数

   名称|内容
   ---|---
   Action|API名称，此例为 `GetUIoTCoreDeviceShadow`。
   PublicKey|用户公钥为`CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTKCmh7Bp5W1UH64D/O`，通过个人中心->API密钥获取。
   Signature|用户签名将在第3步介绍。
   ProjectId|项目ID为 `org-z44lmf12e`，项目ID为 **org-z44lmf12e**，通过控制台首页查看。主账号为空时为默认项目，子账号为必填字段。

3. 获取用户签名  
   用户签名需要接口参数和公共参数以及用户私钥参与一起完成。 

   1） 接口参数+公共参数
   ```
   // 接口参数
   Region:cn-sh2
   ProductSN:8pi2i730vxsala2a
   DeviceSN:ark1d4ug1evfb1jy
   // 公共参数，Signature加密后获取
   Action:GetUIoTCoreDeviceShadow
   PublicKey:CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTKCmh7Bp5W1UH64D/O
   ```
   2）将上述参数按照参数名（上面参数中的`Region、ProjectId`等）进行升序排序
   ```
   Action:GetUIoTCoreDeviceShadow
   DeviceSN:ark1d4ug1evfb1jy
   ProductSN:8pi2i730vxsala2a
   ProjectId:org-z44lmf12e
   PublicKey:CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTKCmh7Bp5W1UH64D/O
   Region:cn-sh2
   ```   
   3）将上述参数的**键值**依次相连构造字符串，并在尾部接上用户私钥
   
   - 用户私钥通过 个人中心->API密钥获取为：`ztqlj0vtg6Por5d/etqpadpTZwscLRh5cIsFAHbwuvnMY4mAWI+GT5C2yzj/KiZf`
   - 拼接获得字符串为（键值依次相连+用户私钥）：
   ```
   ActionGetUIoTCoreDeviceShadowDeviceSNark1d4ug1evfb1jyProductSN8pi2i730vxsala2aProjectIdorg-z44lmf12ePublicKeyCJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTKCmh7Bp5W1UH64D/ORegioncn-sh2ztqlj0vtg6Por5d/etqpadpTZwscLRh5cIsFAHbwuvnMY4mAWI+GT5C2yzj/KiZf
   ```
   4）计算SHA1签名
   
   将第3）步字符串进行SHA1签名，获取签名串为
   ```
   Signature:f1e6b4e35df41b42232e059f6020c7fd51b2889e
   ```
   5）至此所有请求需要的参数
   ```
   Action:GetUIoTCoreDeviceShadow
   DeviceSN:ark1d4ug1evfb1jy
   ProductSN:8pi2i730vxsala2a
   ProjectId:org-z44lmf12e
   PublicKey:CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTKCmh7Bp5W1UH64D/O
   Region:cn-sh2
   Signature:f1e6b4e35df41b42232e059f6020c7fd51b2889e
   ```
4. 请求接口获取响应
   
   通过GET和POST都可以请求接口得到同样的响应结果，请求的BaseURL为`http://api.ucloud.cn/`。

   1）**通过GET方式**  
   ① 当参数中存在特殊字符时需要进行编码，编码的规则为：  
      - 字符 A~Z、a~z、0~9不编码；
      - 字符“-”、“_”、“.”、“~”不编码；
      - 其它字符编码成 %XY 的格式，其中 XY 是字符对应 ASCII 码的 16    进制表示。比如：英文的双引号（”）对应的编码为 %22；
      - 对于扩展的 UTF-8 字符，编码成 %XY%ZA… 的格式；
      - 英文空格（ ）要编码成 %20，而不是加号（+）。
    
    根据上述的规则将
    ```
    PublicKey:CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTKCmh7Bp5W1UH64D/O
    ```
    进行URL编码为
    ```
    PublicKey:CJf%2BLfjjXPk70z%2FfsBlK9sHC%2BkBTTj7gr2g%2FC%2FR7YSi3EFTKCmh7Bp5W1UH64D%2FO
    ```

   ② 将请求参数转换成URL Params，拼接上Base URL进行GET请求：
     ```
     http(s)://api.ucloud.cn/?Action=GetUIoTCoreDeviceShadow&DeviceSN=ark1d4ug1evfb1jy&ProductSN=8pi2i730vxsala2a&ProjectId=org-z44lmf12e&PublicKey=CJf%2BLfjjXPk70z%2FfsBlK9sHC%2BkBTTj7gr2g%2FC%2FR7YSi3EFTKCmh7Bp5W1UH64D%2FO& Region=cn-sh2&Signature=f1e6b4e35df41b42232e059f6020c7fd51b2889e
     ```
   ③ 返回响应结果为：
   ```
   {
    "Action": "GetUIoTCoreDeviceShadowResponse",
    "RetCode": 0,
    "Payload": {
        "State": {
            "Reported": {},
            "Desired": {}
        },
        "Metadata": {
            "Reported": {},
            "Desired": {}
        }
    },
    "Version": 2,
    "Timestamp": 1561011300
   }
   ```
   
   2）**通过POST方式**  
   ① POST通过JSON格式请求：
   ```
   POST  HTTP/1.1
   Host: api.ucloud.cn
   Content-Type: application/json
   Body:
   {
   	"Action": "GetUIoTCoreDeviceShadow",
   	"DeviceSN": "ark1d4ug1evfb1jy",
   	"ProductSN": "8pi2i730vxsala2a",
   	"ProjectId": "org-z44lmf12e",
   	"PublicKey": "CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTK   Cmh7Bp5W1UH64D/O",
   	"Region": "cn-sh2",
   	"Signature": "f1e6b4e35df41b42232e059f6020c7fd51b2889e"
   }
   ```
   ②返回响应结果为：
   ```
   {
    "Action": "GetUIoTCoreDeviceShadowResponse",
    "RetCode": 0,
    "Payload": {
        "State": {
            "Reported": {},
            "Desired": {}
        },
        "Metadata": {
            "Reported": {},
            "Desired": {}
        }
    },
    "Version": 2,
    "Timestamp": 1561011300
   }
   ```
   
## 常见问题
- 当使用GET请求有特殊字符未编码时会出现：
  ```
  {
    "Message": "User Not Exists",
    "RetCode": 172
  }
  ```
- 当签名出错，或者排序出错时会出现：
  ```
  {
    "Message": "Signature VerifyAC Error",
    "RetCode": 171
  }
  ```
- 其他疑问，可以参考[API 文档综览](https://docs.ucloud.cn/api/summary/overview)
