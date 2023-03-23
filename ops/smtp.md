# Mepụta ihe nkesa ozi SMTP nke gị

## okwu mmalite

SMTP nwere ike zụta ọrụ ozugbo n'aka ndị na-ere igwe ojii, dị ka:

* [Amazon SES SMTP](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali ojii email push](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Ị nwekwara ike wuo ihe nkesa ozi gị - enweghị oke nzipu, ọnụ ahịa dị ala.

N'okpuru ebe a, anyị na-egosi nzọụkwụ site nzọụkwụ otu esi ewuo ihe nkesa ozi anyị.

## Nhọrọ nkesa

Ihe nkesa SMTP nke kwadoro onwe ya chọrọ IP ọha nwere ọdụ ụgbọ mmiri 25, 456, na 587 mepere emepe.

Igwe ojii nke ọha na eze na-ejikarị egbochila ọdụ ụgbọ mmiri ndị a na ndabara, yana enwere ike imeghe ha site na ịnye usoro ọrụ, mana ọ na-enye nsogbu mgbe niile.

Ana m akwado ịzụrụ n'aka onye ọbịa nke nwere ọdụ ụgbọ mmiri ndị a meghere ma na-akwado ịtọ aha ngalaba ntụgharị.

N'ebe a, ana m akwado [Contabo](https://contabo.com) .

Contabo bụ onye na-eweta nnabata dabere na Munich, Germany, hiwere na 2003 yana ọnụ ahịa asọmpi.

Ọ bụrụ na ịhọrọ Euro dị ka ego ịzụrụ, ọnụahịa ahụ ga-adị ọnụ ala (ihe nkesa nwere ebe nchekwa 8GB na 4 CPUs na-efu ihe dị ka yuan 529 kwa afọ, ego ntinye mbụ bụ n'efu maka otu afọ).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Mgbe ị na-enye iwu, okwu `prefer AMD` , na ihe nkesa nwere AMD CPU ga-arụ ọrụ nke ọma.

Na ndị na-esonụ, m ga-ewere Contabo's VPS dị ka ihe atụ iji gosi otú e si wuo gị onwe gị nkesa ozi.

## Nhazi sistemụ Ubuntu

Sistemụ arụmọrụ ebe a bụ Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Ọ bụrụ na ihe nkesa na ssh gosipụtara `Welcome to TinyCore 13!` (dị ka egosiri na foto dị n'okpuru ebe a), ọ pụtara na etinyebeghị usoro ahụ. Biko kwụpụ ssh wee chere nkeji ole na ole ka ịbanye ọzọ.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Mgbe `Welcome to Ubuntu 22.04.1 LTS` pụtara, mmalite agwụla, ma ị nwere ike ịga n'ihu na usoro ndị a.

### [Nhọrọ] Bido gburugburu mmepe

Nzọụkwụ a bụ nhọrọ.

Maka ịdị mma, etinyere m nrụnye na nhazi usoro nke ubuntu software na [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

Gbaa iwu na-esonụ ka ịwụnye na otu pịa.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Ndị ọrụ China, biko jiri iwu na-esonụ kama, a ga-edozi asụsụ, mpaghara oge, wdg na-akpaghị aka.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo na-enyere IPV6 aka

Kwado IPV6 ka SMTP nwekwara ike izipu ozi-e na adreesị IPv6.

dezie `/etc/sysctl.conf`

Gbanwee ma ọ bụ tinye ahịrị ndị a

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Soro [nkuzi contabo: Ịtinye njikọ IPv6 na nkesa gị](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Dezie `/etc/netplan/01-netcfg.yaml` , gbakwunye ahịrị ole na ole dị ka egosiri na ọnụ ọgụgụ dị n'okpuru (Contabo VPS faịlụ nhazi nhazi nke nwere ahịrị ndị a, naanị emezighị ha).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Mgbe ahụ `netplan apply` iji mee ka nhazi ahụ gbanwee.

Mgbe nhazi ahụ gachara, ị nwere ike iji `curl 6.ipw.cn` lelee adreesị ipv6 nke netwọk mpụga gị.

## Mechie ops nhazi nhazi

```
git clone https://github.com/wactax/ops.soft.git
```

## N'ịwa a free SSL akwụkwọ n'ihi na gị na ngalaba aha

Izipu ozi chọrọ asambodo SSL maka izo ya ezo na ibinye aka.

Anyị na-eji [acme.sh](https://github.com/acmesh-official/acme.sh) iwepụta asambodo.

acme.sh bụ ngwá ọrụ ntinye akwụkwọ akpaghị aka na-emeghe isi,

Tinye nhazi ụlọ nkwakọba ihe ops.soft, na-agba ọsọ `./ssl.sh` , a ga-emepụta nchekwa `conf` na **ndekọ elu** .

Chọta onye na-eweta DNS gị site na [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , dezie `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Wee na-agba ọsọ `./ssl.sh 123.com` ka ịmepụta `123.com` na `*.123.com` asambodo maka aha ngalaba gị.

Nke mbụ na-agba ọsọ ga-arụnye [acme.sh](https://github.com/acmesh-official/acme.sh) na-akpaghị aka ma gbakwunye ọrụ ahaziri maka mmeghari akpaka. Ị nwere ike ịhụ `crontab -l` , enwere ahịrị dị ka ndị a.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Ụzọ maka asambodo emepụtara bụ ihe dị ka `/mnt/www/.acme.sh/123.com_ecc。`

Asambodo ọhụrụ ga-akpọ `conf/reload/123.com.sh` script, dezie edemede a, ị nwere ike tinye iwu dị ka `nginx -s reload` iji nweta ume cache akwụkwọ nke ngwa ndị metụtara ya.

## Jiri chasquid wuo ihe nkesa SMTP

[chasquid](https://github.com/albertito/chasquid) bụ ihe nkesa SMTP mepere emepe edere n'asụsụ Go.

Dị ka onye nọchiri anya mmemme ihe nkesa ozi oge ochie dị ka Postfix na Sendmail, chasquid dị mfe ma dị mfe iji, ọ dịkwa mfe maka mmepe nke abụọ.

Run `./chasquid/init.sh 123.com` ga-arụnyere na-akpaghị aka na otu click (dochie 123.com na gị iziga ngalaba aha).

## Hazie mbinye aka email DKIM

A na-eji DKIM zipu mbinye aka email iji gbochie a na-emeso akwụkwọ ozi dị ka spam.

Mgbe iwu ahụ gachara nke ọma, a ga-akpali gị ịtọ ndekọ DKIM (dị ka egosiri n'okpuru).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Dị nnọọ tinye a TXT ndekọ gị DNS (dị ka e gosiri n'okpuru).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Lelee ọkwa ọrụ & ndekọ

 `systemctl status chasquid` Lelee ọkwa ọrụ.

Ọnọdụ ọrụ nkịtị dị ka egosiri na foto dị n'okpuru

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` ma ọ bụ `journalctl -xeu chasquid` nwere ike ịlele ndekọ njehie.

## Weghachite ngalaba aha nhazi

The reverse ngalaba aha bụ ikwe ka adreesị IP na-edozi ka kwekọrọ na ngalaba aha.

Ịtọba aha ngalaba ọzọ nwere ike igbochi ozi ịntanetị ka amata ya dị ka spam.

Mgbe enwetara ozi ahụ, ihe nkesa na-enweta ga-eme nyocha ngalaba aha na adreesị IP nke ihe nkesa na-ezipụ iji gosi ma ihe nkesa na-ezipụ nwere aha ngalaba ntụgharị dị irè.

Ọ bụrụ na ihe nkesa na-ezipụ enweghị aha ngalaba ntụgharị ma ọ bụ ọ bụrụ na aha ngalaba ahụ adabaghị na adreesị IP nke ihe nkesa na-ezipụ, ihe nkesa na-enweta nwere ike ịmata email ahụ dị ka spam ma ọ bụ jụ ya.

Gaa na [https://my.contabo.com/rdns](https://my.contabo.com/rdns) wee hazie dị ka egosiri n'okpuru

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Mgbe mwube reverse ngalaba aha, cheta hazi ebugharị mkpebi nke ngalaba aha ipv4 na ipv6 na ihe nkesa.

## Dezie aha nnabata nke chasquid.conf

Gbanwee `conf/chasquid/chasquid.conf` ka uru nke aha ngalaba azụ.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Wee mee `systemctl restart chasquid` ka ịmalitegharị ọrụ ahụ.

## Ndabere conf gaa na ebe nchekwa git

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Dịka ọmụmaatụ, ana m akwado nchekwa conf na usoro github nke m dị ka ndị a

Buru ụzọ mepụta ụlọ nkwakọba ihe nkeonwe

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Tinye ndekọ conf wee nyefee n'ụlọ nkwakọba ihe

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Tinye onye zitere

na-agba ọsọ

```
chasquid-util user-add i@wac.tax
```

Enwere ike ịgbakwunye onye na-ezipụ

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Nyochaa na edobere okwuntughe nke ọma

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Mgbe ịgbakwunye onye ọrụ, `chasquid/domains/wac.tax/users` ga-emelite, cheta idobe ya n'ụlọ nkwakọba ihe.

## DNS tinye ndekọ SPF

SPF ( Nhazi Amụma nke izipu ) bụ teknụzụ nkwenye email ejiri egbochi wayo email.

Ọ na-enyocha njirimara nke onye na-ezigara ozi site na ịlele na adreesị IP onye na-ezite ya kwekọrọ na ndekọ DNS nke ngalaba aha ọ na-ekwu na ọ bụ, na-egbochi ndị wayo izipu ozi ịntanetị adịgboroja.

Ịtinye ndekọ SPF nwere ike igbochi ozi ịntanetị ka a mata ya dị ka spam dị ka o kwere mee.

Ọ bụrụ na gị na ngalaba aha nkesa na-adịghị akwado SPF ụdị, dị nnọọ tinye TXT ụdị ndekọ.

Dịka ọmụmaatụ, SPF nke `wac.tax` bụ nke a

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF maka `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Rịba ama na m nwere `include:_spf.google.com` ebe a, nke a bụ n'ihi na m ga-ahazi `i@wac.tax` dị ka adreesị izipu na igbe ozi Google ma emechaa.

## Nhazi DNS DMARC

DMARC bụ mbiri nke (Nchọpụta ozi dabere na ngalaba, mkpesa na nkwenye).

A na-eji ya weghara bounces SPF (ikekwe kpatara njehie nhazi, ma ọ bụ onye ọzọ na-eme ka ọ bụrụ na ị na-eziga spam).

Tinye ndekọ TXT `_dmarc` ,

Ọdịnaya dị ka ndị a

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Ihe nkebi nke ọ bụla pụtara bụ nke a

### p (Iwu)

Na-egosi otu esi ejikwa ozi-e na-ada SPF (Nhazi amụma ezipụ) ma ọ bụ DKIM (DomainKeys Identified Mail). Enwere ike ịtọ paramita p ka ọ bụrụ otu n'ime ụkpụrụ atọ:

* Ọ dịghị ihe ọ bụla: Ọ dịghị ihe e mere, naanị nkwenye nkwenye na-enyeghachi onye zitere ya site na usoro mkpesa email.
* Kwarantaini: Tinye mail nke na-agafebeghị nkwenye ahụ n'ime folda spam, mana agaghị ajụ mail ozugbo.
* jụrụ: Jụ ozugbo ozi-e na-adaghị nkwenye.

### maka (Nhọrọ ọdịda)

Na-akọwapụta ọnụọgụ ozi nke usoro mkpesa weghachiri. Enwere ike ịtọ ya ka ọ bụrụ otu ụkpụrụ ndị a:

* 0: Kpesa nsonaazụ nkwado maka ozi niile
* 1: Naanị kọọ ozi na-ada nkwenye
* d: Naanị kọọ ọdịda nkwenye aha ngalaba
* s: naanị na-akọ ọdịda nkwenye SPF
* l: Naanị gosi ọdịda nkwenye DKIM

### rua & ruf

* rua (URI na-akọ maka mkpesa mkpokọta): Adreesị ozi-e maka ịnata akụkọ ekpokọtara
* ruf (URI na-akọ maka akụkọ gbasara amụma): adreesị ozi-e iji nweta akụkọ zuru ezu

## Tinye ndekọ MX iji zipu ozi-e na Google Mail

N'ihi na enweghị m ike ịchọta igbe ozi ụlọ ọrụ efu na-akwado adreesị ụwa niile (Catch-All, nwere ike ịnweta ozi-e ọ bụla ezigara na ngalaba aha a, na-enweghị mgbochi na prefixes), ejiri m chasquid ziga ozi-e niile na igbe ozi Gmail m.

**Ọ bụrụ na ị nwere igbe ozi azụmahịa a na-akwụ ụgwọ nke gị, biko emezigharịla MX wee mafee nzọụkwụ a.**

Dezie `conf/chasquid/domains/wac.tax/aliases` , tọọ igbe ozi mbugharị

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` na-egosi ozi-e niile, a bụ `i` prefix adreesị ozi-e nke onye na-ezipụ ozi emepụtara n'elu. Iji zipu ozi, onye ọrụ ọ bụla kwesịrị ịgbakwunye ahịrị.

Wee tinye ndekọ MX (m na-atụ aka ozugbo na adreesị nke ngalaba aha azụ ebe a, dị ka egosiri na ahịrị mbụ na ọnụ ọgụgụ dị n'okpuru).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Mgbe nhazi ahụ mechara, ị nwere ike iji adreesị ozi-e ndị ọzọ iji zipu ozi-e na `i@wac.tax` na `any123@wac.tax` iji hụ ma ị nwere ike ịnweta ozi-e na Gmail.

Ọ bụrụ na ọ bụghị, lelee ndekọ chasquid ( `grep chasquid /var/log/syslog` ).

## Jiri Google Mail ziga email na i@wac.tax

Mgbe Google Mail natara ozi ahụ, enwere m olile anya ịza `i@wac.tax` kama i.wac.tax@gmail.com.

Gaa na [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) wee pịa "Tinye adreesị ozi-e ọzọ".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Mgbe ahụ, tinye koodu nkwenye enwetara site na ozi-e ezigara ya.

N'ikpeazụ, enwere ike ịtọ ya dị ka adreesị ezipụ nke ndabara (yana nhọrọ iji otu adreesị zaghachi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

N'ụzọ dị otú a, anyị emechala nguzobe nke SMTP mail server ma n'otu oge ahụ na-eji Google Mail izipu na-enweta ozi ịntanetị.

## Zipụ ozi-e nwale ka ịlele ma nhazi ahụ ọ na-aga nke ọma

Tinye `ops/chasquid`

Gbaa `direnv allow` ka ịwụnye ịdabere (direnv etinyere na usoro mmalite otu igodo gara aga ma tinye nko na shei)

wee gbaa ọsọ

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Ihe paramita pụtara dị ka ndị a

* onye ọrụ: SMTP aha njirimara
* ngafe: SMTP paswọọdụ
* ka: onye nnata

Ị nwere ike izipu email ule.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

A na-atụ aro ka iji Gmail nweta ozi-e nwale iji lelee ma nhazi ahụ ọ na-aga nke ọma.

### TLS ọkọlọtọ nzuzo

Dịka egosiri na foto dị n'okpuru, enwere obere mkpọchi a, nke pụtara na ejirila asambodo SSL rụọ ọrụ nke ọma.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Wee pịa "Gosi Email izizi"

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

Dị ka egosiri na foto dị n'okpuru, Gmail akwụkwọ ozi mbụ gosipụtara DKIM, nke pụtara na nhazi DKIM na-aga nke ọma.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Lelee ihe enwetara na nkụnye eji isi mee nke ozi-e mbụ, ma ị ga-ahụ na adreesị onye zitere bụ IPV6, nke pụtara na ahaziri IPV6 nke ọma.
