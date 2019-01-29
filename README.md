# Tobet BlackJack Verify

验证工具网页请访问：https://tobetone.github.io/BlackJack/

在使用此网页工具之前，请仔细阅读以下说明。你可以根据如下说明，自行开发程序验证。
## 开奖结果计算
  1. 根据游戏数据生成随机种子,并签名：<br>
    seed = GameId+BetUserNum+BetPlayersACCount+BetAmount*10000+LastBetTime;<br>
    seed_sign = sign(seed)<br>
  2. 对随机种子hash（SH256）运算，结果转换为16进制<br>
    hash_hex = hex(sha256(seed_sign))<br>
  3. 获取牌组下标后拿出牌<br>
    for(var i=0;i<49;i++){<br>
    　　var signHash = parseInt(hash.substr(i,6),16);<br>
    　　var index = Math.abs(signHash % (208-i));<br>
    }


## 随机因子说明
   seed = GameId+BetUserNum+BetPlayersACCount+BetAmount*10000+LastBetTime;
*  GameId:游戏ID
*  BetUserNum:下注总人数
*  BetPlayersACCount:参与游戏玩家账号拼接
*  BetAmoun:本局游戏玩家总投注金额
*  LastBetTime:玩家的投注时间
## 签名验证
   验证签名使用Tobet的公钥（EOS6CG8VwJ8G1iFn6x781PMojmfD7i4kqqzsgd1AjWwAaEz35QGhn），对seed_sign进行ecc签名验证，验证结果通过即可证明随机种子未被篡改。
