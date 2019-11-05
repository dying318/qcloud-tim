# qcloud-tim

2019-11-05 Forked from [xutl/qcloud-tim](https://github.com/xutl/qcloud-tim), 部分功能优化

腾讯云 TIM 云通信SDK，支持 同步 异步模式。


## Installation

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist dying318/qcloud-tim
```

or add

```
"dying318/qcloud-tim": "~1.0"
```

to the require section of your `composer.json` file.

## Use

```php
use XuTL\QCloud\Tim\Tim;
use XuTL\QCloud\Tim\Constants;

$client = new Tim(
    '1234557',
    '12341234',
    '13241234/j8/341234+HOcet3Of1cTErNDm9XubwIeAyO0YE1bQFWNn+Iyc4',
    'MFYwEAYHKoZIzj0CAQYF134K4EEAAoDQgAEmV31rGrO12341234TRcQJLu+8w689UYMxsZE06WUKwEQCCwCBh6PhznHrdzn9XExKzQ5vV7m8CHgMjtGBNW0BVjZ/iMnOA==',
    'webmaster'
);

//操作用户
$account = $client->getAccount('test112');
//获取用户资料
$profile = $account->getProfile();
//T下线
$account->kick();

//查询在线状态
$account->state();

//更多接口请看 
XuTL\QCloud\Tim\Account 类

// 好有关系操作
$friend = $client->getFirend('accountId')
// 检查黑名单关系
$result = $friend->blackCheck(['checkAccount1'], Constants::BLACK_CHECK_RESULT_TYPE_BOTH);
if ($result->isSucceed()) {
    $checkContent = $result->getContent();
} 

//群组操作
$group = $client->getGroup('test');

//修改圈子属性
$groupAttributes = new GroupAttributes();
$groupAttributes->setName('方圆百里找对手');
$groupAttributes->setApplyJoinOption(Constants::GROUP_APPLY_JOIN_OPTION_FREE_ACCESS);
try {
    $res = $group->setInfo($groupAttributes);
    print_r($res);
} catch (\XuTL\QCloud\Tim\Exception\TIMException $e) {
    print_r($e->getMessage());
}
//更多圈子接口请看 
XuTL\QCloud\Tim\Group 类
```

