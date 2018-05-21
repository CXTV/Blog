# urlencode方法



```
import re
import json
from urllib.parse import urlencode

def params():

    params = []
    html = 'jsonp18({"data":{"availableUser":true,"csrfID":"152574263739202216372477268409266","isTmall":true,"loginUser":{"contentStatus":1,"ext":"From ZuanShi Site","grayStatus":10,"itemcpcStatus":1,"nickname":"健足乐旗舰","operId":3919666792,"operName":"健足乐旗舰:伟禄","operType":2,"shopId":569771360,"userId":131356172,"userNumId":3881573568,"userStatus":0,"zuanshiStatus":1},"memberConfig":[],"permission":{"AlgoAutoCreativePermission":false,"CMOPermission":true,"DiagnosePermission":true,"RptCmoAdvancedRoiPermission":false,"RptCmoAdvancedRoiPermissionGray":false,"bannerComponent":true,"budgetAlertPermission":true,"budgetSimulator":true,"cmsPagePermission":true,"dmpCrowdPermission":false,"dmpMenuPermission":false,"dmpToZuanshi":true,"hostingBannerCpc":true,"hostingBannerNew":true,"hostingBannerNormal":true,"hostingItemNormal":true,"intelligentBidPermission":true,"isAgencyCust":false,"isHaveTopAppCampaign":false,"isJnNoCrowdMember":false,"isMemberRefundByChannel":true,"isTmallMember":false,"itemComponent":true,"marketAutoBid":true,"marketingDemandPermission":true,"ocpcBannerPermission":true,"ocpmPurchase":true,"priceSimulator":true,"priceSimulatorPPC":true,"productPermission":{"productContent":{},"productItemCpc":{"campaignModelList":[4],"productId":101004014},"productLive":{},"productZuanshi":{"campaignModelList":[1],"productId":101004013}},"recommendBannerNew":true,"recommendBannerNormal":true},"reportUrl":"https://report.simba.taobao.com/","rptToken":"健足乐旗舰:伟禄.3881573568.131356172.2.29488ccf","sign":false,"userShopMainCatId":50006843,"userZsAdboardCatId":3},"info":{"isDisableTime":false,"isLockSla":false,"ok":true}})'
    content = re.search('{"data(.*)', html).group()[:-1]
    data = json.loads(content)
    csrf = data['data']['csrfID']
    rpt = data['data']['rptToken']
    token = urlencode({'token':rpt},encoding='utf-8')
    params.append(csrf)
    params.append(token)

    return params

print(params()[0],params()[1])
```

