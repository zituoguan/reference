---
title: HTML 字符实体
date: 2022-01-13 11:44:21
tags:
  - html
  - code
  - characters
categories:
  - 其他
intro: |
  本速查表是 HTML 实体的完整列表，包含它们的数字和名称。此外，还包括了可以在 HTML 中表示的 ASCII 字符的完整列表。
---

## HTML 字符实体引用 {.cols-1}

### HTML 特殊字符

| HTML       | 符号   | 数字     | 描述                   | 十六进制      | CSS (ISO) | JS (八进制)                                               |
| ---------- | ------ | -------- | ---------------------- | ------------- | --------- | --------------------------------------------------------- |
| `&quot;`   | "      | `&#34;`  | 引号                   | u+0022 ISOnum | \\0022    | <a href='javascript:alert(&quot;\42&quot;)'>\42</a>       |
| `&num;`    | #      | `&#35;`  | 数字符号               | u+0023 ISOnum | \\0023    | <a href='javascript:alert(&quot;\43&quot;)'>\43</a>       |
| `&dollar;` | $      | `&#36;`  | 美元符号               | u+0024 ISOnum | \\0024    | <a href='javascript:alert(&quot;\44&quot;)'>\44</a>       |
| `&percnt;` | %      | `&#37;`  | 百分号                 | u+0025 ISOnum | \\0025    | <a href='javascript:alert(&quot;\45&quot;)'>\45</a>       |
| `&amp;`    | &      | `&#38;`  | 和号                   | u+0026 ISOnum | \\0026    | <a href='javascript:alert(&quot;\46&quot;)'>\46</a>       |
| `&apos;`   | '      | `&#39;`  | 撇号                   | u+0027 ISOnum | \\0027    | <a href='javascript:alert(&quot;\47&quot;)'>\47</a>       |
| `&lpar;`   | (      | `&#40;`  | 左括号                 | u+0028 ISOnum | \\0028    | <a href='javascript:alert(&quot;\50&quot;)'>\50</a>       |
| `&rpar;`   | )      | `&#41;`  | 右括号                 | u+0029 ISOnum | \\0029    | <a href='javascript:alert(&quot;\51&quot;)'>\51</a>       |
| `&ast;`    | \*     | `&#42;`  | 星号                   | u+002A ISOnum | \\002a    | <a href='javascript:alert(&quot;\52&quot;)'>\52</a>       |
| `&plus;`   | +      | `&#43;`  | 加号                   | u+002B ISOnum | \\002b    | <a href='javascript:alert(&quot;\53&quot;)'>\53</a>       |
| `&comma;`  | ,      | `&#44;`  | 逗号                   | u+002C ISOnum | \\002c    | <a href='javascript:alert(&quot;\54&quot;)'>\54</a>       |
| `&minus;`  | -      | `&#45;`  | 连字符减号             | u+002D ISOnum | \\002d    | <a href='javascript:alert(&quot;\55&quot;)'>\55</a>       |
| `&period;` | .      | `&#46;`  | 句号                   | u+002E ISOnum | \\002e    | <a href='javascript:alert(&quot;\56&quot;)'>\56</a>       |
| `&sol;`    | /      | `&#47;`  | 斜杠                   | u+002F ISOnum | \\002f    | <a href='javascript:alert(&quot;\57&quot;)'>\57</a>       |
| `&colon;`  | :      | `&#58;`  | 冒号                   | u+003A ISOnum | \\003a    | <a href='javascript:alert(&quot;\72&quot;)'>\72</a>       |
| `&semi;`   | ;      | `&#59;`  | 分号                   | u+003B ISOnum | \\003b    | <a href='javascript:alert(&quot;\73&quot;)'>\73</a>       |
| `&lt;`     | <      | `&#60;`  | 小于号                 | u+003C ISOnum | \\003c    | <a href='javascript:alert(&quot;\74&quot;)'>\74</a>       |
| `&equals;` | =      | `&#61;`  | 等号                   | u+003D ISOnum | \\003d    | <a href='javascript:alert(&quot;\75&quot;)'>\75</a>       |
| `&gt;`     | >      | `&#62;`  | 大于号                 | u+003E ISOnum | \\003e    | <a href='javascript:alert(&quot;\76&quot;)'>\76</a>       |
| `&quest;`  | ?      | `&#63;`  | 问号                   | u+003F ISOnum | \\003f    | <a href='javascript:alert(&quot;\77&quot;)'>\77</a>       |
| `&commat;` | @      | `&#64;`  | @符号；商业@           | u+0040 ISOnum | \\0040    | <a href='javascript:alert(&quot;\100&quot;)'>\100</a>     |
| `&lsqb;`   | [      | `&#91;`  | 左方括号               | u+005B ISOnum | \\005b    | <a href='javascript:alert(&quot;\133&quot;)'>\133</a>     |
| `&bsol;`   | \      | `&#92;`  | 反斜杠                 | u+005C ISOnum | \\005c    | <a href='javascript:alert(&quot;\134&quot;)'>\134</a>     |
| `&rsqb;`   | ]      | `&#93;`  | 右方括号               | u+005D ISOnum | \\005d    | <a href='javascript:alert(&quot;\135&quot;)'>\135</a>     |
| `&Hat;`    | ^      | `&#94;`  | 扬抑符；脱字符         | u+005E ISOnum | \\005e    | <a href='javascript:alert(&quot;\136&quot;)'>\136</a>     |
| `&lowbar;` | \_     | `&#95;`  | 下划线                 | u+005F ISOnum | \\005f    | <a href='javascript:alert(&quot;\137&quot;)'>\137</a>     |
| `&grave;`  | &#96;  | `&#96;`  | 重音符                 | u+0060 ISOnum | \\0060    | <a href='javascript:alert(&quot;\u0060&quot;)'>\u0060</a> |
| `&lcub;`   | {      | `&#123;` | 左花括号               | u+007b ISOnum | \\007b    | <a href='javascript:alert(&quot;\173&quot;)'>\173</a>     |
| `&verbar;` | \|     | `&#124;` | 竖线                   | u+007c ISOnum | \\007c    | <a href='javascript:alert(&quot;\174&quot;)'>\174</a>     |
| `&rcub;`   | }      | `&#125;` | 右花括号               | u+007d ISOnum | \\007d    | <a href='javascript:alert(&quot;\175&quot;)'>\175</a>     |
|            | ~      | `&#126;` | 波浪号                 | u+007e ISOnum | \\007e    | <a href='javascript:alert(&quot;\176&quot;)'>\176</a>     |

{.show-header}

### HTML 拉丁字符

| HTML       | 符号   | 数字       | 描述                               | 十六进制 | CSS (ISO) | JS (八进制)                                               |
| ---------- | ------ | ---------- | ---------------------------------- | ------ | --------- | --------------------------------------------------------- |
| `&nbsp;`   |        | `&#160;`   | 不间断空格                         | %A0    | \\00a0    | <a href='javascript:alert(&quot;\240&quot;)'>\240</a>     |
| `&iexcl;`  | ¡      | `&#161;`   | 反向感叹号                         | %A1    | \\00a1    | <a href='javascript:alert(&quot;\241&quot;)'>\241</a>     |
| `&cent;`   | ¢      | `&#162;`   | 分币符号                           | %A2    | \\00a2    | <a href='javascript:alert(&quot;\242&quot;)'>\242</a>     |
| `&pound;`  | £      | `&#163;`   | 英镑符号                           | %A3    | \\00a3    | <a href='javascript:alert(&quot;\243&quot;)'>\243</a>     |
| `&curren;` | ¤      | `&#164;`   | 通用货币符号                       | %A4    | \\00a4    | <a href='javascript:alert(&quot;\244&quot;)'>\244</a>     |
| `&yen;`    | ¥      | `&#165;`   | 日元符号                           | %A5    | \\00a5    | <a href='javascript:alert(&quot;\245&quot;)'>\245</a>     |
| `&#x20B9;` | ₹      | `&#x20B9;` | 印度卢比符号                       | U+20B9 | \\20B9    | <a href='javascript:alert(&quot;\u20B9&quot;)'>\u20B9</a> |
| `&brvbar;` | ¦      | `&#166;`   | 断的竖线；断杠                     | %A6    | \\00a6    | <a href='javascript:alert(&quot;\246&quot;)'>\246</a>     |
| `&sect;`   | §      | `&#167;`   | 节符号                             | %A7    | \\00a7    | <a href='javascript:alert(&quot;\247&quot;)'>\247</a>     |
| `&uml;`    | ¨      | `&#168;`   | 元音变音符（分音符）               | %A8    | \\00a8    | <a href='javascript:alert(&quot;\250&quot;)'>\250</a>     |
| `&copy;`   | ©     | `&#169;`   | 版权符号                           | %A9    | \\00a9    | <a href='javascript:alert(&quot;\251&quot;)'>\251</a>     |
| `&ordf;`   | ª      | `&#170;`   | 序数指示符，阴性                   | %AA    | \\00aa    | <a href='javascript:alert(&quot;\252&quot;)'>\252</a>     |
| `&laquo;`  | «      | `&#171;`   | 左尖角引号                         | %AB    | \\00ab    | <a href='javascript:alert(&quot;\253&quot;)'>\253</a>     |
| `&not;`    | ¬      | `&#172;`   | 非符号                             | %AC    | \\00ac    | <a href='javascript:alert(&quot;\254&quot;)'>\254</a>     |
| `&shy;`    | ­      | `&#173;`   | 软连字符                           | %AD    | \\00ad    | <a href='javascript:alert(&quot;\255&quot;)'>\255</a>     |
| `&reg;`    | ®     | `&#174;`   | 注册商标符号                       | %AE    | \\00ae    | <a href='javascript:alert(&quot;\256&quot;)'>\256</a>     |
| `&macr;`   | ¯      | `&#175;`   | 长音符号                           | %AF    | \\00af    | <a href='javascript:alert(&quot;\257&quot;)'>\257</a>     |
| `&deg;`    | °      | `&#176;`   | 度符号                             | %B0    | \\00b0    | <a href='javascript:alert(&quot;\260&quot;)'>\260</a>     |
| `&plusmn;` | ±      | `&#177;`   | 加减号                             | %B1    | \\00b1    | <a href='javascript:alert(&quot;\261&quot;)'>\261</a>     |
| `&sup2;`   | ²      | `&#178;`   | 上标 2                             | %B2    | \\00b2    | <a href='javascript:alert(&quot;\262&quot;)'>\262</a>     |
| `&sup3;`   | ³      | `&#179;`   | 上标 3                             | %B3    | \\00b3    | <a href='javascript:alert(&quot;\263&quot;)'>\263</a>     |
| `&acute;`  | ´      | `&#180;`   | 锐音符                             | %B4    | \\00b4    | <a href='javascript:alert(&quot;\264&quot;)'>\264</a>     |
| `&micro;`  | µ      | `&#181;`   | 微符号                             | %B5    | \\00b5    | <a href='javascript:alert(&quot;\265&quot;)'>\265</a>     |
| `&para;`   | ¶      | `&#182;`   | 段落符号                           | %B6    | \\00b6    | <a href='javascript:alert(&quot;\266&quot;)'>\266</a>     |
| `&middot;` | ·      | `&#183;`   | 中点                               | %B7    | \\00b7    | <a href='javascript:alert(&quot;\267&quot;)'>\267</a>     |
| `&cedil;`  | ¸      | `&#184;`   | 软音符                             | %B8    | \\00b8    | <a href='javascript:alert(&quot;\270&quot;)'>\270</a>     |
| `&sup1;`   | ¹      | `&#185;`   | 上标 1                             | %B9    | \\00b9    | <a href='javascript:alert(&quot;\271&quot;)'>\271</a>     |
| `&ordm;`   | º      | `&#186;`   | 序数指示符，阳性                   | %BA    | \\00ba    | <a href='javascript:alert(&quot;\272&quot;)'>\272</a>     |
| `&raquo;`  | »      | `&#187;`   | 右尖角引号                         | %BB    | \\00bb    | <a href='javascript:alert(&quot;\273&quot;)'>\273</a>     |
| `&frac14;` | ¼      | `&#188;`   | 四分之一                           | %BC    | \\00bc    | <a href='javascript:alert(&quot;\274&quot;)'>\274</a>     |
| `&frac12;` | ½      | `&#189;`   | 二分之一                           | %BD    | \\00bd    | <a href='javascript:alert(&quot;\275&quot;)'>\275</a>     |
| `&frac34;` | ¾      | `&#190;`   | 四分之三                           | %BE    | \\00be    | <a href='javascript:alert(&quot;\276&quot;)'>\276</a>     |
| `&iquest;` | ¿      | `&#191;`   | 反向问号                           | %BF    | \\00bf    | <a href='javascript:alert(&quot;\277&quot;)'>\277</a>     |
| `&Agrave;` | À      | `&#192;`   | 大写 A，重音符                     | %C0    | \\00c0    | <a href='javascript:alert(&quot;\300&quot;)'>\300</a>     |
| `&Aacute;` | Á      | `&#193;`   | 大写 A，锐音符                     | %C1    | \\00c1    | <a href='javascript:alert(&quot;\301&quot;)'>\301</a>     |
| `&Acirc;`  | Â      | `&#194 ;`  | 大写 A，扬抑符                     | %C2    | \\00c2    | <a href='javascript:alert(&quot;\302&quot;)'>\302</a>     |
| `&Atilde;` | Ã      | `&#195;`   | 大写 A，波浪号                     | %C3    | \\00c3    | <a href='javascript:alert(&quot;\303&quot;)'>\303</a>     |
| `&Auml;`   | Ä      | `&#196;`   | 大写 A，分音符或元音变音符         | %C4    | \\00c4    | <a href='javascript:alert(&quot;\304&quot;)'>\304</a>     |
| `&Aring;`  | Å      | `&#197;`   | 大写 A，上圆圈                     | %C5    | \\00c5    | <a href='javascript:alert(&quot;\305&quot;)'>\305</a>     |
| `&AElig;`  | Æ      | `&#198;`   | 大写 AE 连字                       | %C6    | \\00c6    | <a href='javascript:alert(&quot;\306&quot;)'>\306</a>     |
| `&Ccedil;` | Ç      | `&#199;`   | 大写 C，软音符                     | %C7    | \\00c7    | <a href='javascript:alert(&quot;\307&quot;)'>\307</a>     |
| `&Egrave;` | È      | `&#200;`   | 大写 E，重音符                     | %C8    | \\00c8    | <a href='javascript:alert(&quot;\310&quot;)'>\310</a>     |
| `&Eacute;` | É      | `&#201;`   | 大写 E，锐音符                     | %C9    | \\00c9    | <a href='javascript:alert(&quot;\311&quot;)'>\311</a>     |
| `&Ecirc;`  | Ê      | `&#202;`   | 大写 E，扬抑符                     | %CA    | \\00ca    | <a href='javascript:alert(&quot;\312&quot;)'>\312</a>     |
| `&Euml;`   | Ë      | `&#203;`   | 大写 E，分音符或元音变音符         | %CB    | \\00cb    | <a href='javascript:alert(&quot;\313&quot;)'>\313</a>     |
| `&Igrave;` | Ì      | `&#204;`   | 大写 I，重音符                     | %CC    | \\00cc    | <a href='javascript:alert(&quot;\314&quot;)'>\314</a>     |
| `&Iacute;` | Í      | `&#205;`   | 大写 I，锐音符                     | %CD    | \\00cd    | <a href='javascript:alert(&quot;\315&quot;)'>\315</a>     |
| `&Icirc;`  | Î      | `&#206;`   | 大写 I，扬抑符                     | %CE    | \\00ce    | <a href='javascript:alert(&quot;\316&quot;)'>\316</a>     |
| `&Iuml;`   | Ï      | `&#207;`   | 大写 I，分音符或元音变音符         | %CF    | \\00cf    | <a href='javascript:alert(&quot;\317&quot;)'>\317</a>     |
| `&ETH;`    | Ð      | `&#208;`   | 大写 Eth，冰岛语                   | %D0    | \\00d0    | <a href='javascript:alert(&quot;\320&quot;)'>\320</a>     |
| `&Ntilde;` | Ñ      | `&#209;`   | 大写 N，波浪号                     | %D1    | \\00d1    | <a href='javascript:alert(&quot;\321&quot;)'>\321</a>     |
| `&Ograve;` | Ò      | `&#210;`   | 大写 O，重音符                     | %D2    | \\00d2    | <a href='javascript:alert(&quot;\322&quot;)'>\322</a>     |
| `&Oacute;` | Ó      | `&#211;`   | 大写 O，锐音符                     | %D3    | \\00d3    | <a href='javascript:alert(&quot;\323&quot;)'>\323</a>     |
| `&Ocirc;`  | Ô      | `&#212;`   | 大写 O，扬抑符                     | %D4    | \\00d4    | <a href='javascript:alert(&quot;\324&quot;)'>\324</a>     |
| `&Otilde;` | Õ      | `&#213;`   | 大写 O，波浪号                     | %D5    | \\00d5    | <a href='javascript:alert(&quot;\325&quot;)'>\325</a>     |
| `&Ouml;`   | Ö      | `&#214;`   | 大写 O，分音符或元音变音符         | %D6    | \\00d6    | <a href='javascript:alert(&quot;\326&quot;)'>\326</a>     |
| `&times;`  | ×      | `&#215;`   | 乘号                               | %D7    | \\00d7    | <a href='javascript:alert(&quot;\327&quot;)'>\327</a>     |
| `&Oslash;` | Ø      | `&#216;`   | 大写 O，带斜杠                     | %D8    | \\00d8    | <a href='javascript:alert(&quot;\330&quot;)'>\330</a>     |
| `&Ugrave;` | Ù      | `&#217;`   | 大写 U，重音符                     | %D9    | \\00d9    | <a href='javascript:alert(&quot;\331&quot;)'>\331</a>     |
| `&Uacute;` | Ú      | `&#218;`   | 大写 U，锐音符                     | %DA    | \\00da    | <a href='javascript:alert(&quot;\332&quot;)'>\332</a>     |
| `&Ucirc;`  | Û      | `&#219;`   | 大写 U，扬抑符                     | %DB    | \\00db    | <a href='javascript:alert(&quot;\333&quot;)'>\333</a>     |
| `&Uuml;`   | Ü      | `&#220;`   | 大写 U，分音符或元音变音符         | %DC    | \\00dc    | <a href='javascript:alert(&quot;\334&quot;)'>\334</a>     |
| `&Yacute;` | Ý      | `&#221;`   | 大写 Y，锐音符                     | %DD    | \\00dd    | <a href='javascript:alert(&quot;\335&quot;)'>\335</a>     |
| `&THORN;`  | Þ      | `&#222;`   | 大写 THORN，冰岛语                 | %DE    | \\00de    | <a href='javascript:alert(&quot;\336&quot;)'>\336</a>     |
| `&szlig;`  | ß      | `&#223;`   | 小写清音 s，德语（sz 连字）        | %DF    | \\00df    | <a href='javascript:alert(&quot;\337&quot;)'>\337</a>     |
| `&agrave;` | à      | `&#224;`   | 小写 a，重音符                     | %E0    | \\00e0    | <a href='javascript:alert(&quot;\340&quot;)'>\340</a>     |
| `&aacute;` | á      | `&#225;`   | 小写 a，锐音符                     | %E1    | \\00e1    | <a href='javascript:alert(&quot;\341&quot;)'>\341</a>     |
| `&acirc;`  | â      | `&#226;`   | 小写 a，扬抑符                     | %E2    | \\00e2    | <a href='javascript:alert(&quot;\342&quot;)'>\342</a>     |
| `&atilde;` | ã      | `&#227;`   | 小写 a，波浪号                     | %E3    | \\00e3    | <a href='javascript:alert(&quot;\343&quot;)'>\343</a>     |
| `&auml;`   | ä      | `&#228;`   | 小写 a，分音符或元音变音符         | %E4    | \\00e4    | <a href='javascript:alert(&quot;\344&quot;)'>\344</a>     |
| `&aring;`  | å      | `&#229;`   | 小写 a，上圆圈                     | %E5    | \\00e5    | <a href='javascript:alert(&quot;\345&quot;)'>\345</a>     |
| `&aelig;`  | æ      | `&#230;`   | 小写 ae 连字                       | %E6    | \\00e6    | <a href='javascript:alert(&quot;\346&quot;)'>\346</a>     |
| `&ccedil;` | ç      | `&#231;`   | 小写 c，软音符                     | %E7    | \\00e7    | <a href='javascript:alert(&quot;\347&quot;)'>\347</a>     |
| `&egrave;` | è      | `&#232;`   | 小写 e，重音符                     | %E8    | \\00e8    | <a href='javascript:alert(&quot;\350&quot;)'>\350</a>     |
| `&eacute;` | é      | `&#233;`   | 小写 e，锐音符                     | %E9    | \\00e9    | <a href='javascript:alert(&quot;\351&quot;)'>\351</a>     |
| `&ecirc;`  | ê      | `&#234;`   | 小写 e，扬抑符                     | %EA    | \\00ea    | <a href='javascript:alert(&quot;\352&quot;)'>\352</a>     |
| `&euml;`   | ë      | `&#235;`   | 小写 e，分音符或元音变音符         | %EB    | \\00eb    | <a href='javascript:alert(&quot;\353&quot;)'>\353</a>     |
| `&igrave;` | ì      | `&#236;`   | 小写 i，重音符                     | %EC    | \\00ec    | <a href='javascript:alert(&quot;\354&quot;)'>\354</a>     |
| `&iacute;` | í      | `&#237;`   | 小写 i，锐音符                     | %ED    | \\00ed    | <a href='javascript:alert(&quot;\355&quot;)'>\355</a>     |
| `&icirc;`  | î      | `&#238;`   | 小写 i，扬抑符                     | %EE    | \\00ee    | <a href='javascript:alert(&quot;\356&quot;)'>\356</a>     |
| `&iuml;`   | ï      | `&#239;`   | 小写 i，分音符或元音变音符         | %EF    | \\00ef    | <a href='javascript:alert(&quot;\357&quot;)'>\357</a>     |
| `&eth;`    | ð      | `&#240;`   | 小写 eth，冰岛语                   | %F0    | \\00f0    | <a href='javascript:alert(&quot;\360&quot;)'>\360</a>     |
| `&ntilde;` | ñ      | `&#241;`   | 小写 n，波浪号                     | %F1    | \\00f1    | <a href='javascript:alert(&quot;\361&quot;)'>\361</a>     |
| `&ograve;` | ò      | `&#242;`   | 小写 o，重音符                     | %F2    | \\00f2    | <a href='javascript:alert(&quot;\362&quot;)'>\362</a>     |
| `&oacute;` | ó      | `&#243;`   | 小写 o，锐音符                     | %F3    | \\00f3    | <a href='javascript:alert(&quot;\363&quot;)'>\363</a>     |
| `&ocirc;`  | ô      | `&#244;`   | 小写 o，扬抑符                     | %F4    | \\00f4    | <a href='javascript:alert(&quot;\364&quot;)'>\364</a>     |
| `&otilde;` | õ      | `&#245;`   | 小写 o，波浪号                     | %F5    | \\00f5    | <a href='javascript:alert(&quot;\365&quot;)'>\365</a>     |
| `&ouml;`   | ö      | `&#246;`   | 小写 o，分音符或元音变音符         | %F6    | \\00f6    | <a href='javascript:alert(&quot;\366&quot;)'>\366</a>     |
| `&divide;` | ÷      | `&#247;`   | 除号                               | %F7    | \\00f7    | <a href='javascript:alert(&quot;\367&quot;)'>\367</a>     |
| `&oslash;` | ø      | `&#248;`   | 小写 o，带斜杠                     | %F8    | \\00f8    | <a href='javascript:alert(&quot;\370&quot;)'>\370</a>     |
| `&ugrave;` | ù      | `&#249;`   | 小写 u，重音符                     | %F9    | \\00f9    | <a href='javascript:alert(&quot;\371&quot;)'>\371</a>     |
| `&uacute;` | ú      | `&#250;`   | 小写 u，锐音符                     | %FA    | \\00fa    | <a href='javascript:alert(&quot;\372&quot;)'>\372</a>     |
| `&ucirc;`  | û      | `&#251;`   | 小写 u，扬抑符                     | %FB    | \\00fb    | <a href='javascript:alert(&quot;\373&quot;)'>\373</a>     |
| `&uuml;`   | ü      | `&#252;`   | 小写 u，分音符或元音变音符         | %FC    | \\00fc    | <a href='javascript:alert(&quot;\374&quot;)'>\374</a>     |
| `&yacute;` | ý      | `&#253;`   | 小写 y，锐音符                     | %FD    | \\00fd    | <a href='javascript:alert(&quot;\375&quot;)'>\375</a>     |
| `&thorn;`  | þ      | `&#254;`   | 小写 thorn，冰岛语                 | %FE    | \\00fe    | <a href='javascript:alert(&quot;\376&quot;)'>\376</a>     |
| `&yuml;`   | ÿ      | `&#255;`   | 小写 y，分音符或元音变音符         | %FF    | \\00ff    | <a href='javascript:alert(&quot;\377&quot;)'>\377</a>     |

{.show-header}

### HTML 拉丁字符扩展

| HTML       | 符号   | 数字     | 描述                                | 十六进制       | CSS (ISO) | JS (八进制)                                               |
| ---------- | ------ | -------- | ----------------------------------- | -------------- | --------- | --------------------------------------------------------- |
| `&OElig;`  | Œ      | `&#338;` | 拉丁大写连字 oe                     | u+0152 ISOlat2 | \\0152    | <a href='javascript:alert(&quot;\u0152&quot;)'>\u0152</a> |
| `&oelig;`  | œ      | `&#339;` | 拉丁小写连字 oe                     | u+0153 ISOlat2 | \\0153    | <a href='javascript:alert(&quot;\u0153&quot;)'>\u0153</a> |
| `&Scaron;` | Š      | `&#352;` | 带分音符的大写拉丁字母 S            | u+0160 ISOlat2 | \\0160    | <a href='javascript:alert(&quot;\u0160&quot;)'>\u0160</a> |
| `&scaron;` | š      | `&#353;` | 带分音符的小写拉丁字母 s            | u+0161 ISOlat2 | \\0161    | <a href='javascript:alert(&quot;\u0161&quot;)'>\u0161</a> |
| `&Yuml;`   | Ÿ      | `&#376;` | 带分音符的大写拉丁字母 Y            | u+0178 ISOlat2 | \\0178    | <a href='javascript:alert(&quot;\u0178&quot;)'>\u0178</a> |
| `&fnof;`   | ƒ      | `&#402;` | 带钩的小写拉丁字母 f                | u+0192 ISOtech | \\0192    | <a href='javascript:alert(&quot;\u0192&quot;)'>\u0192</a> |

{.show-header}

### HTML 间距修饰字符

| HTML      | 符号   | 数字     | 描述                                | 十六进制      | CSS (ISO) | JS (八进制)                                               |
| --------- | ------ | -------- | ----------------------------------- | ------------- | --------- | --------------------------------------------------------- |
| `&circ;`  | ˆ      |          | 修饰符扬抑符                        | u+02C6 ISOpub | \\02c6    | <a href='javascript:alert(&quot;\u02c6&quot;)'>\u02c6</a> |
| `&tilde;` | ˜      |          | 小波浪号                            | u+02DC ISOdia | \\02dc    | <a href='javascript:alert(&quot;\u02dc&quot;)'>\u02dc</a> |

{.show-header}

### HTML 希腊字符

| HTML         | 符号   | 数字     | 描述                                | 十六进制       | CSS (ISO) | JS (八进制)                                               |
| ------------ | ------ | -------- | --------------------------------- | -------------- | --------- | --------------------------------------------------------- |
| `&Alpha;`    | Α      | `&#913;` | 希腊大写字母 Alpha                  | u+0391         | \\0391    | <a href='javascript:alert(&quot;\u0391&quot;)'>\u0391</a> |
| `&Beta;`     | Β      | `&#914;` | 希腊大写字母 Beta                   | u+0392         | \\0392    | <a href='javascript:alert(&quot;\u0392&quot;)'>\u0392</a> |
| `&Gamma;`    | Γ      | `&#915;` | 希腊大写字母 Gamma                  | u+0393 ISOgrk3 | \\0393    | <a href='javascript:alert(&quot;\u0395&quot;)'>\u0395</a> |
| `&Delta;`    | Δ      | `&#916;` | 希腊大写字母 Delta                  | u+0394 ISOgrk3 | \\0394    | <a href='javascript:alert(&quot;\u0394&quot;)'>\u0394</a> |
| `&Epsilon;`  | Ε      | `&#917;` | 希腊大写字母 Epsilon                | u+0395         | \\0395    | <a href='javascript:alert(&quot;\u0395&quot;)'>\u0395</a> |
| `&Zeta;`     | Ζ      | `&#918;` | 希腊大写字母 Zeta                   | u+0396         | \\0396    | <a href='javascript:alert(&quot;\u0396&quot;)'>\u0396</a> |
| `&Eta;`      | Η      | `&#919;` | 希腊大写字母 Eta                    | u+0397         | \\0397    | <a href='javascript:alert(&quot;\u0397&quot;)'>\u0397</a> |
| `&Theta;`    | Θ      | `&#920;` | 希腊大写字母 Theta                  | u+0398 ISOgrk3 | \\0398    | <a href='javascript:alert(&quot;\u0398&quot;)'>\u0398</a> |
| `&Iota;`     | Ι      | `&#921;` | 希腊大写字母 Iota                   | u+0399         | \\0399    | <a href='javascript:alert(&quot;\u0399&quot;)'>\u0399</a> |
| `&Kappa;`    | Κ      | `&#922;` | 希腊大写字母 Kappa                  | u+039A         | \\039a    | <a href='javascript:alert(&quot;\u039a&quot;)'>\u039a</a> |
| `&Lambda;`   | Λ      | `&#923;` | 希腊大写字母 Lambda                 | u+039B ISOgrk3 | \\039b    | <a href='javascript:alert(&quot;\u039b&quot;)'>\u039b</a> |
| `&Mu;`       | Μ      | `&#924;` | 希腊大写字母 Mu                     | u+039C         | \\039c    | <a href='javascript:alert(&quot;\u039c&quot;)'>\u039c</a> |
| `&Nu;`       | Ν      | `&#925;` | 希腊大写字母 Nu                     | u+039D         | \\039d    | <a href='javascript:alert(&quot;\u039D&quot;)'>\u039D</a> |
| `&Xi;`       | Ξ      | `&#926;` | 希腊大写字母 Xi                     | u+039E ISOgrk3 | \\039e    | <a href='javascript:alert(&quot;\u039e&quot;)'>\u039e</a> |
| `&Omicron;`  | Ο      | `&#927;` | 希腊大写字母 Omicron                | u+039F         | \\039f    | <a href='javascript:alert(&quot;\u039f&quot;)'>\u039f</a> |
| `&Pi;`       | Π      | `&#928;` | 希腊大写字母 Pi                     | u+03A0 ISOgrk3 | \\03a0    | <a href='javascript:alert(&quot;\u03a0&quot;)'>\u03a0</a> |
| `&Rho;`      | Ρ      | `&#929;` | 希腊大写字母 Rho                    | u+03A1         | \\03a1    | <a href='javascript:alert(&quot;\u03a1&quot;)'>\u03a1</a> |
| `&Sigma;`    | Σ      | `&#931;` | 希腊大写字母 Sigma                  | u+03A3 ISOgrk3 | \\03a3    | <a href='javascript:alert(&quot;\u03A3&quot;)'>\u03A3</a> |
| `&Tau;`      | Τ      | `&#932;` | 希腊大写字母 Tau                    | u+03A4         | \\03a4    | <a href='javascript:alert(&quot;\u03A4&quot;)'>\u03A4</a> |
| `&Upsilon;`  | Υ      | `&#933;` | 希腊大写字母 Upsilon                | u+03A5 ISOgrk3 | \\03a5    | <a href='javascript:alert(&quot;\u03A5&quot;)'>\u03A5</a> |
| `&Phi;`      | Φ      | `&#934;` | 希腊大写字母 Phi                    | u+03A6 ISOgrk3 | \\03a6    | <a href='javascript:alert(&quot;\u03A6&quot;)'>\u03A6</a> |
| `&Chi;`      | Χ      | `&#935;` | 希腊大写字母 Chi                    | u+03A7         | \\03a7    | <a href='javascript:alert(&quot;\u03A7&quot;)'>\u03A7</a> |
| `&Psi;`      | Ψ      | `&#936;` | 希腊大写字母 Psi                    | u+03A8 ISOgrk3 | \\03a8    | <a href='javascript:alert(&quot;\u03A8&quot;)'>\u03A8</a> |
| `&Omega;`    | Ω      | `&#937;` | 希腊大写字母 Omega                  | u+03A9 ISOgrk3 | \\03a9    | <a href='javascript:alert(&quot;\u03A9&quot;)'>\u03A9</a> |
| `&alpha;`    | α      | `&#945;` | 希腊小写字母 alpha                  | u+03B1 ISOgrk3 | \\03b1    | <a href='javascript:alert(&quot;\u03b1&quot;)'>\u03b1</a> |
| `&beta;`     | β      | `&#946;` | 希腊小写字母 beta                   | u+03B2 ISOgrk3 | \\03b2    | <a href='javascript:alert(&quot;\u03b2&quot;)'>\u03b2</a> |
| `&gamma;`    | γ      | `&#947;` | 希腊小写字母 gamma                  | u+03B3 ISOgrk3 | \\03b3    | <a href='javascript:alert(&quot;\u03b3&quot;)'>\u03b3</a> |
| `&delta;`    | δ      | `&#948;` | 希腊小写字母 delta                  | u+03B4 ISOgrk3 | \\03b4    | <a href='javascript:alert(&quot;\u03b4&quot;)'>\u03b4</a> |
| `&epsilon;`  | ε      | `&#949;` | 希腊小写字母 epsilon                | u+03B5 ISOgrk3 | \\03b5    | <a href='javascript:alert(&quot;\u03b5&quot;)'>\u03b5</a> |
| `&zeta;`     | ζ      | `&#950;` | 希腊小写字母 zeta                   | u+03B6 ISOgrk3 | \\03b6    | <a href='javascript:alert(&quot;\u03b6&quot;)'>\u03b6</a> |
| `&eta;`      | η      | `&#951;` | 希腊小写字母 eta                    | u+03B7 ISOgrk3 | \\03b7    | <a href='javascript:alert(&quot;\u03b7&quot;)'>\u03b7</a> |
| `&theta;`    | θ      | `&#952;` | 希腊小写字母 theta                  | u+03B8 ISOgrk3 | \\03b8    | <a href='javascript:alert(&quot;\u03b8&quot;)'>\u03b8</a> |
| `&iota;`     | ι      | `&#953;` | 希腊小写字母 iota                   | u+03B9 ISOgrk3 | \\03b9    | <a href='javascript:alert(&quot;\u03b9&quot;)'>\u03b9</a> |
| `&kappa;`    | κ      | `&#954;` | 希腊小写字母 kappa                  | u+03BA ISOgrk3 | \\03ba    | <a href='javascript:alert(&quot;\u03ba&quot;)'>\u03ba</a> |
| `&lambda;`   | λ      | `&#955;` | 希腊小写字母 lambda                 | u+03BB ISOgrk3 | \\03bb    | <a href='javascript:alert(&quot;\u03bb&quot;)'>\u03bb</a> |
| `&mu;`       | μ      | `&#956;` | 希腊小写字母 mu                     | u+03BC ISOgrk3 | \\03bc    | <a href='javascript:alert(&quot;\u03bc&quot;)'>\u03bc</a> |
| `&nu;`       | ν      | `&#957;` | 希腊小写字母 nu                     | u+03BD ISOgrk3 | \\03bd    | <a href='javascript:alert(&quot;\u03bd&quot;)'>\u03bd</a> |
| `&xi;`       | ξ      | `&#958;` | 希腊小写字母 xi                     | u+03BE ISOgrk3 | \\03be    | <a href='javascript:alert(&quot;\u03be&quot;)'>\u03be</a> |
| `&omicron;`  | ο      | `&#959;` | 希腊小写字母 omicron                | u+03BF NEW     | \\03bf    | <a href='javascript:alert(&quot;\u03bf&quot;)'>\u03bf</a> |
| `&pi;`       | π      | `&#960;` | 希腊小写字母 pi                     | u+03C0 ISOgrk3 | \\03c0    | <a href='javascript:alert(&quot;\u03c0&quot;)'>\u03c0</a> |
| `&rho;`      | ρ      | `&#961;` | 希腊小写字母 rho                    | u+03C1 ISOgrk3 | \\03c1    | <a href='javascript:alert(&quot;\u03c1&quot;)'>\u03c1</a> |
| `&sigmaf;`   | ς      | `&#962;` | 希腊小写字母 final sigma            | u+03C2 ISOgrk3 | \\03C2    | <a href='javascript:alert(&quot;\u03c2&quot;)'>\u03c2</a> |
| `&sigma;`    | σ      | `&#963;` | 希腊小写字母 sigma                  | u+03C3 ISOgrk3 | \\03C3    | <a href='javascript:alert(&quot;\u03c3&quot;)'>\u03c3</a> |
| `&tau;`      | τ      | `&#964;` | 希腊小写字母 tau                    | u+03C4 ISOgrk3 | \\03C4    | <a href='javascript:alert(&quot;\u03c4&quot;)'>\u03c4</a> |
| `&upsilon;`  | υ      | `&#965;` | 希腊小写字母 upsilon                | u+03C5 ISOgrk3 | \\03C5    | <a href='javascript:alert(&quot;\u03c5&quot;)'>\u03c5</a> |
| `&phi;`      | φ      | `&#966;` | 希腊小写字母 phi                    | u+03C6 ISOgrk3 | \\03C6    | <a href='javascript:alert(&quot;\03c6&quot;)'>\03c6</a>   |
| `&chi;`      | χ      | `&#967;` | 希腊小写字母 chi                    | u+03C7 ISOgrk3 | \\03C7    | <a href='javascript:alert(&quot;\u03c7&quot;)'>\u03c7</a> |
| `&psi;`      | ψ      | `&#968;` | 希腊小写字母 psi                    | u+03C8 ISOgrk3 | \\03C8    | <a href='javascript:alert(&quot;\u03c8&quot;)'>\u03c8</a> |
| `&omega;`    | ω      | `&#969;` | 希腊小写字母 omega                  | u+03C9 ISOgrk3 | \\03C9    | <a href='javascript:alert(&quot;\u03c9&quot;)'>\u03c9</a> |
| `&thetasym;` | ϑ      | `&#977;` | 希腊小写字母 theta 符号             | u+03D1 NEW     | \\03D1    | <a href='javascript:alert(&quot;\u03D1&quot;)'>\u03D1</a> |
| `&upsih;`    | ϒ      | `&#978;` | 带钩的希腊字母 upsilon 符号         | u+03D2 NEW     | \\03D2    | <a href='javascript:alert(&quot;\u03D2&quot;)'>\u03D2</a> |
| `&piv;`      | ϖ      | `&#982;` | 希腊 pi 符号                        | u+03D6 ISOgrk3 | \\03D6    | <a href='javascript:alert(&quot;\u03D6&quot;)'>\u03D6</a> |

{.show-header}

### HTML 标点符号

| HTML       | 符号   | 数字      | 描述                                               | 十六进制            | CSS (ISO) | JS (八进制)                                               |
| ---------- | ------ | --------- | -------------------------------------------------- | ------------------- | --------- | --------------------------------------------------------- |
| `&ensp;`   |        | `&#8194;` | en 空格                                            | u+2002 ISOpub       | \\2002    | <a href='javascript:alert(&quot;\u2002&quot;)'>\u2002</a> |
| `&emsp;`   |        | `&#8195;` | em 空格                                            | u+2003 ISOpub       | \\2003    | <a href='javascript:alert(&quot;\u2003&quot;)'>\u2003</a> |
| `&thinsp;` |        | `&#8201;` | 窄空格                                             | u+2009 ISOpub       | \\2009    | <a href='javascript:alert(&quot;\u2009&quot;)'>\u2009</a> |
| `&zwnj;`   | ‌      | `&#8204;` | 零宽度非连接符                                     | u+200C NEW RFC 2070 | \\200C    | <a href='javascript:alert(&quot;\u200C&quot;)'>\u200C</a> |
| `&zwj;`    | ‍      | `&#8205;` | 零宽度连接符                                       | u+200D NEW RFC 2070 | \\200D    | <a href='javascript:alert(&quot;\u200d&quot;)'>\u200d</a> |
| `&lrm;`    | ‎      | `&#8206;` | 从左到右标记                                       | u+200E NEW RFC 2070 | \\200E    | <a href='javascript:alert(&quot;\u200e&quot;)'>\u200e</a> |
| `&rlm;`    | ‏      | `&#8207;` | 从右到左标记                                       | u+200F NEW RFC 2070 | \\200F    | <a href='javascript:alert(&quot;\u200f&quot;)'>\u200f</a> |
| `&ndash;`  | –      | `&#8211;` | en 破折号                                          | u+2013 ISOpub       | \\2013    | <a href='javascript:alert(&quot;\u2013&quot;)'>\u2013</a> |
| `&mdash;`  | —      | `&#8212;` | em 破折号                                          | u+2014 ISOpub       | \\2014    | <a href='javascript:alert(&quot;\u2014&quot;)'>\u2014</a> |
| `&lsquo;`  | ‘      | `&#8216;` | 左单引号                                           | u+2018 ISOnum       | \\2018    | <a href='javascript:alert(&quot;\u2018&quot;)'>\u2018</a> |
| `&rsquo;`  | ’      | `&#8217;` | 右单引号                                           | u+2019 ISOnum       | \\2019    | <a href='javascript:alert(&quot;\u2019&quot;)'>\u2019</a> |
| `&sbquo;`  | ‚      | `&#8218;` | 单低 9 引号                                        | u+201A NEW          | \\201A    | <a href='javascript:alert(&quot;\u201a&quot;)'>\u201a</a> |
| `&ldquo;`  | “      | `&#8220;` | 左双引号                                           | u+201C ISOnum       | \\201C    | <a href='javascript:alert(&quot;\u201c&quot;)'>\u201c</a> |
| `&rdquo;`  | ”      | `&#8221;` | 右双引号                                           | u+201D ISOnum       | \\201D    | <a href='javascript:alert(&quot;\u201d&quot;)'>\u201d</a> |
| `&bdquo;`  | „      | `&#8222;` | 双低 9 引号                                        | u+201E NEW          | \\201E    | <a href='javascript:alert(&quot;\u201e&quot;)'>\u201e</a> |
| `&dagger;` | †      | `&#8224;` | 剑号                                               | u+2020 ISOpub       | \\2020    | <a href='javascript:alert(&quot;\u2020&quot;)'>\u2020</a> |
| `&Dagger;` | ‡      | `&#8225;` | 双剑号                                             | u+2021 ISOpub       | \\2021    | <a href='javascript:alert(&quot;\u2021&quot;)'>\u2021</a> |
| `&permil;` | ‰      | `&#8240;` | 千分号                                             | u+2030 ISOtech      | \\2030    | <a href='javascript:alert(&quot;\u2030&quot;)'>\u2030</a> |
| `&lsaquo;` | ‹      | `&#8249;` | 单左尖角引号                                       | u+2039 ISO proposed | \\2039    | <a href='javascript:alert(&quot;\u2039&quot;)'>\u2039</a> |
| `&rsaquo;` | ›      | `&#8250;` | 单右尖角引号                                       | u+203A ISO proposed | \\203A    | <a href='javascript:alert(&quot;\u203a&quot;)'>\u203a</a> |
| `&bull;`   | •      | `&#8226;` | 项目符号，又称黑色小圆圈                           | u+2022 ISOpub       | \\2022    | <a href='javascript:alert(&quot;\u2219&quot;)'>\u2219</a> |
| `&hellip;` | …      | `&#8230;` | 水平省略号，又称三点前导符                         | u+2026 ISOpub       | \\2026    | <a href='javascript:alert(&quot;\u2026&quot;)'>\u2026</a> |
| `&prime;`  | ′      | `&#8242;` | 角分符号，又称分钟，又称英尺                       | u+2032 ISOtech      | \\2032    | <a href='javascript:alert(&quot;\u2032&quot;)'>\u2032</a> |
| `&Prime;`  | ″      | `&#8243;` | 角秒符号，又称秒，又称英寸                         | u+2033 ISOtech      | \\2033    | <a href='javascript:alert(&quot;\u2033&quot;)'>\u2033</a> |
| `&oline;`  | ‾      | `&#8254;` | 上划线，又称间隔上划线                             | u+203E NEW          | \\203E    | <a href='javascript:alert(&quot;\u203e&quot;)'>\u203e</a> |
| `&frasl;`  | ⁄      | `&#8260;` | 分数斜杠                                           | u+2044 NEW          | \\2044    | <a href='javascript:alert(&quot;\u8260&quot;)'>\u8260</a> |

{.show-header}

### HTML 类字母符号

| HTML        | 符号   | 数字      | 描述                                                       | 十六进制       | CSS (ISO) | JS (八进制)                                               |
| ----------- | ------ | --------- | ---------------------------------------------------------- | -------------- | --------- | --------------------------------------------------------- |
| `&weierp;`  | ℘      | `&#8472;` | 手写体大写 P，又称幂集，又称魏尔斯特拉斯 p                 | u+2118 ISOamso | \\2118    | <a href='javascript:alert(&quot;\u2118&quot;)'>\u2118</a> |
| `&image;`   | ℑ      | `&#8465;` | 黑体大写 I，又称虚部                                       | u+2111 ISOamso | \\2111    | <a href='javascript:alert(&quot;\u2111&quot;)'>\u2111</a> |
| `&real;`    | ℜ      | `&#8476;` | 黑体大写 R，又称实部符号                                   | u+211C ISOamso | \\211C    | <a href='javascript:alert(&quot;\u211c&quot;)'>\u211c</a> |
| `&trade;`   | ™     | `&#8482;` | 商标符号                                                   | u+2122 ISOnum  | \\2122    | <a href='javascript:alert(&quot;\u2122&quot;)'>\u2122</a> |
| `&alefsym;` | ℵ      | `&#8501;` | 阿列夫符号                                                 | u+2135 NEW     | \\2135    | <a href='javascript:alert(&quot;\u&quot;)'>\u</a>         |

{.show-header}

### HTML 箭头

| HTML      | 符号   | 数字      | 描述                                                       | 十六进制       | CSS (ISO) | JS (八进制)                                               |
| --------- | ------ | --------- | ---------------------------------------------------------- | -------------- | --------- | --------------------------------------------------------- |
| `&larr;`  | ←      | `&#8592;` | 左箭头                                                     | u+2190 ISOnum  | \\2190    | <a href='javascript:alert(&quot;\u2190&quot;)'>\u2190</a> |
| `&uarr;`  | ↑      | `&#8593;` | 上箭头                                                     | u+2191 ISOnum  | \\2191    | <a href='javascript:alert(&quot;\u2191&quot;)'>\u2191</a> |
| `&rarr;`  | →      | `&#8594;` | 右箭头                                                     | u+2192 ISOnum  | \\2192    | <a href='javascript:alert(&quot;\u2192&quot;)'>\u2192</a> |
| `&darr;`  | ↓      | `&#8595;` | 下箭头                                                     | u+2193 ISOnum  | \\2193    | <a href='javascript:alert(&quot;\u2193&quot;)'>\u2193</a> |
| `&harr;`  | ↔     | `&#8596;` | 左右箭头                                                   | u+2194 ISOamsa | \\2194    | <a href='javascript:alert(&quot;\u2194&quot;)'>\u2194</a> |
| `&crarr;` | ↵      | `&#8629;` | 左下弯箭头，又称回车                                       | u+21B5 NEW     | \\21B5    | <a href='javascript:alert(&quot;\u21b5&quot;)'>\u21b5</a> |
| `&lArr;`  | ⇐      | `&#8656;` | 双左箭头，可用于“被…蕴含”                                  | u+21D0 ISOtech | \\21D0    | <a href='javascript:alert(&quot;\u21d0&quot;)'>\u21d0</a> |
| `&uArr;`  | ⇑      | `&#8657;` | 双上箭头                                                   | u+21D1 ISOamsa | \\21D1    | <a href='javascript:alert(&quot;\u21d1&quot;)'>\u21d1</a> |
| `&rArr;`  | ⇒      | `&#8658;` | 双右箭头                                                   | u+21D2 ISOtech | \\21D2    | <a href='javascript:alert(&quot;\u21d2&quot;)'>\u21d2</a> |
| `&dArr;`  | ⇓      | `&#8659;` | 双下箭头                                                   | u+21D3 ISOamsa | \\21D3    | <a href='javascript:alert(&quot;\ud1d3&quot;)'>\ud1d3</a> |
| `&hArr;`  | ⇔      | `&#8660;` | 双左右箭头                                                 | u+21D4 ISOamsa | \\21D4    | <a href='javascript:alert(&quot;\u21d4&quot;)'>\u21d4</a> |
|           | ◄      | `&#9668;` | 黑色左指向三角形                                           | U+25C0         | \\25C0    | <a href='javascript:alert(&quot;\u25c0&quot;)'>\u25c0</a> |
|           | ►      | `&#9658;` | 黑色右指向三角形                                           | u+25B6         | \\25b6    | <a href='javascript:alert(&quot;\u25b6&quot;)'>\u25b6</a> |
|           | ▲      | `&#9650;` | 黑色上指向三角形                                           | u+25B2         | \\25b2    | <a href='javascript:alert(&quot;\25b2&quot;)'>\25b2</a>   |
|           | ▼      | `&#9660;` | 黑色下指向三角形                                           | u+25BC         | \\25bc    | <a href='javascript:alert(&quot;\25bc&quot;)'>\25bc</a>   |

{.show-header}

### HTML 数学运算符

| HTML       | 符号   | 数字      | 描述                                                       | 十六进制       | CSS (ISO) | JS (八进制)                                               |
| ---------- | ------ | --------- | ---------------------------------------------------------- | -------------- | --------- | --------------------------------------------------------- |
| `&forall;` | ∀      | `&#8704;` | 全称量词（对于所有）                                       | u+2200 ISOtech | \\2200    | <a href='javascript:alert(&quot;\u2200&quot;)'>\u2200</a> |
| `&part;`   | ∂      | `&#8706;` | 偏微分                                                     | u+2202 ISOtech | \\2202    | <a href='javascript:alert(&quot;\u2202&quot;)'>\u2202</a> |
| `&exist;`  | ∃      | `&#8707;` | 存在量词（存在）                                           | u+2203 ISOtech | \\2203    | <a href='javascript:alert(&quot;\u2203&quot;)'>\u2203</a> |
| `&empty;`  | ∅      | `&#8709;` | 空集，又称直径                                             | u+2205 ISOamso | \\2205    | <a href='javascript:alert(&quot;\u2205&quot;)'>\u2205</a> |
| `&nabla;`  | ∇      | `&#8711;` | Nabla 算子，又称梯度算子                                   | u+2207 ISOtech | \\2207    | <a href='javascript:alert(&quot;\u2207&quot;)'>\u2207</a> |
| `&isin;`   | ∈      | `&#8712;` | 属于                                                       | u+2208 ISOtech | \\2208    | <a href='javascript:alert(&quot;\u2208&quot;)'>\u2208</a> |
| `&notin;`  | ∉      | `&#8713;` | 不属于                                                     | u+2209 ISOtech | \\2209    | <a href='javascript:alert(&quot;\u2209&quot;)'>\u2209</a> |
| `&ni;`     | ∋      | `&#8715;` | 包含（作为成员）                                           | u+220B ISOtech | \\220B    | <a href='javascript:alert(&quot;\u220b&quot;)'>\u220b</a> |
| `&prod;`   | ∏      | `&#8719;` | n 元乘积，又称乘积符号                                     | u+220F ISOamsb | \\220F    | <a href='javascript:alert(&quot;\u03a0&quot;)'>\u03a0</a> |
| `&sum;`    | ∑      | `&#8721;` | n 元求和                                                   | u+2211 ISOamsb | \\2211    | <a href='javascript:alert(&quot;\u03a3&quot;)'>\u03a3</a> |
| `&minus;`  | −      | `&#8722;` | 减号                                                       | u+2212 ISOtech | \\2212    | <a href='javascript:alert(&quot;\u2212&quot;)'>\u2212</a> |
| `&lowast;` | ∗      | `&#8727;` | 星号运算符                                                 | u+2217 ISOtech | \\2217    | <a href='javascript:alert(&quot;\u2217&quot;)'>\u2217</a> |
| `&radic;`  | √      | `&#8730;` | 平方根，又称根号                                           | u+221A ISOtech | \\221A    | <a href='javascript:alert(&quot;\u221a&quot;)'>\u221a</a> |
| `&prop;`   | ∝      | `&#8733;` | 正比于                                                     | u+221D ISOtech | \\221D    | <a href='javascript:alert(&quot;\u221d&quot;)'>\u221d</a> |
| `&infin;`  | ∞      | `&#8734;` | 无穷大                                                     | u+221E ISOtech | \\221E    | <a href='javascript:alert(&quot;\u221e&quot;)'>\u221e</a> |
| `&ang;`    | ∠      | `&#8736;` | 角                                                         | u+2220 ISOamso | \\2220    | <a href='javascript:alert(&quot;\u2220&quot;)'>\u2220</a> |
| `&and;`    | ⊥      | `&#8869;` | 逻辑与，又称楔形                                           | u+2227 ISOtech | \\2227    | <a href='javascript:alert(&quot;\u2227&quot;)'>\u2227</a> |
| `&or;`     | ⊦      | `&#8870;` | 逻辑或，又称 V 形                                          | u+2228 ISOtech | \\2228    | <a href='javascript:alert(&quot;\u2228&quot;)'>\u2228</a> |
| `&cap;`    | ∩      | `&#8745;` | 交集，又称帽形                                             | u+2229 ISOtech | \\2229    | <a href='javascript:alert(&quot;\u2229&quot;)'>\u2229</a> |
| `&cup;`    | ∪      | `&#8746;` | 并集，又称杯形                                             | u+222A ISOtech | \\222A    | <a href='javascript:alert(&quot;\u222a&quot;)'>\u222a</a> |
| `&int;`    | ∫      | `&#8747;` | 积分                                                       | u+222B ISOtech | \\222B    | <a href='javascript:alert(&quot;\u222b&quot;)'>\u222b</a> |
| `&there4;` | ∴      | `&#8756;` | 所以                                                       | u+2234 ISOtech | \\2234    | <a href='javascript:alert(&quot;\u2234&quot;)'>\u2234</a> |
| `&sim;`    | ∼      | `&#8764;` | 波浪号（相似）                                             | u+223C ISOtech | \\223C    | <a href='javascript:alert(&quot;\u223c&quot;)'>\u223c</a> |
| `&cong;`   | ≅      | `&#8773;` | 约等于                                                     | u+2245 ISOtech | \\2245    | <a href='javascript:alert(&quot;\u2245&quot;)'>\u2245</a> |
| `&asymp;`  | ≈      | `&#8776;` | 近似等于，又称渐近于                                       | u+2248 ISOamsr | \\2248    | <a href='javascript:alert(&quot;\u2248&quot;)'>\u2248</a> |
| `&ne;`     | ≠      | `&#8800;` | 不等于                                                     | u+2260 ISOtech | \\2260    | <a href='javascript:alert(&quot;\u2260&quot;)'>\u2260</a> |
| `&equiv;`  | ≡      | `&#8801;` | 恒等于                                                     | u+2261 ISOtech | \\2261    | <a href='javascript:alert(&quot;\u2261&quot;)'>\u2261</a> |
| `&le;`     | ≤      | `&#8804;` | 小于或等于                                                 | u+2264 ISOtech | \\2264    | <a href='javascript:alert(&quot;\u2264&quot;)'>\u2264</a> |
| `&ge;`     | ≥      | `&#8805;` | 大于或等于                                                 | u+2265 ISOtech | \\2265    | <a href='javascript:alert(&quot;\u2265&quot;)'>\u2265</a> |
| `&sub;`    | ⊂      | `&#8834;` | 子集                                                       | u+2282 ISOtech | \\2282    | <a href='javascript:alert(&quot;\u2282&quot;)'>\u2282</a> |
| `&sup;`    | ⊃      | `&#8835;` | 超集                                                       | u+2283 ISOtech | \\2283    | <a href='javascript:alert(&quot;\u2283&quot;)'>\u2283</a> |
| `&nsub;`   | ⊄      | `&#8836;` | 非子集                                                     | u+2284 ISOamsn | \\2284    | <a href='javascript:alert(&quot;\u2284&quot;)'>\u2284</a> |
| `&sube;`   | ⊆      | `&#8838;` | 子集或等于                                                 | u+2286 ISOtech | \\2286    | <a href='javascript:alert(&quot;\u2286&quot;)'>\u2286</a> |
| `&supe;`   | ⊇      | `&#8839;` | 超集或等于                                                 | u+2287 ISOtech | \\2287    | <a href='javascript:alert(&quot;\u2287&quot;)'>\u2287</a> |
| `&oplus;`  | ⊕      | `&#8853;` | 圆圈加号，又称直和                                         | u+2295 ISOamsb | \\2295    | <a href='javascript:alert(&quot;\u2295&quot;)'>\u2295</a> |
| `&otimes;` | ⊗      | `&#8855;` | 圆圈乘号，又称向量积                                       | u+2297 ISOamsb | \\2297    | <a href='javascript:alert(&quot;\u2297&quot;)'>\u2297</a> |
| `&perp;`   | ⊥      | `&#8869;` | 上丁字（垂直）                                             | u+22A5 ISOtech | \\22A5    | <a href='javascript:alert(&quot;\u22a5&quot;)'>\u22a5</a> |
| `&sdot;`   | ⋅      | `&#8901;` | 点运算符                                                   | u+22C5 ISOamsb | \\22C5    | <a href='javascript:alert(&quot;\u22c5&quot;)'>\u22c5</a> |

{.show-header}

### HTML 技术符号

| HTML       | 符号   | 数字      | 描述                                                       | 十六进制       | CSS (ISO) | JS (八进制)                                               |
| ---------- | ------ | --------- | ---------------------------------------------------------- | -------------- | --------- | --------------------------------------------------------- |
| `&lceil;`  | ⌈      | `&#8968;` | 左顶，又称 apl 上柱                                        | u+2308 ISOamsc | \\2308    | <a href='javascript:alert(&quot;\u2308&quot;)'>\u2308</a> |
| `&rceil;`  | ⌉      | `&#8969;` | 右顶                                                       | u+2309 ISOamsc | \\2309    | <a href='javascript:alert(&quot;\u2309&quot;)'>\u2309</a> |
| `&lfloor;` | ⌊      | `&#8970;` | 左底，又称 apl 下柱                                        | u+230A ISOamsc | \\230A    | <a href='javascript:alert(&quot;\u230a&quot;)'>\u230a</a> |
| `&rfloor;` | ⌋      | `&#8971;` | 右底                                                       | u+230B ISOamsc | \\230B    | <a href='javascript:alert(&quot;\u230b&quot;)'>\u230b</a> |
| `&lang;`   | 〈     | `&#9001;` | 左尖括号                                                   | u+2329 ISOtech | \\2329    | <a href='javascript:alert(&quot;\u2329&quot;)'>\u2329</a> |
| `&rang;`   | 〉     | `&#9002;` | 右尖括号                                                   | u+232A ISOtech | \\232A    | <a href='javascript:alert(&quot;\u232a&quot;)'>\u232a</a> |

{.show-header}

### HTML 其他符号

| HTML       | 符号   | 数字      | 描述                                                       | 十六进制      | CSS (ISO) | JS (八进制)                                               |
| ---------- | ------ | --------- | ---------------------------------------------------------- | ------------- | --------- | --------------------------------------------------------- |
| `&loz;`    | ◊      | `&#9674;` | 菱形                                                       | u+25CA ISOpub | \\25CA    | <a href='javascript:alert(&quot;\u25ca&quot;)'>\u25ca</a> |
| `&spades;` | ♠     | `&#9824;` | 黑桃                                                       | u+2660 ISOpub | \\2660    | <a href='javascript:alert(&quot;\u2660&quot;)'>\u2660</a> |
| `&clubs;`  | ♣     | `&#9827;` | 梅花，又称三叶草                                           | u+2663 ISOpub | \\2663    | <a href='javascript:alert(&quot;\u2663&quot;)'>\u2663</a> |
| `&hearts;` | ♥     | `&#9829;` | 红心，又称情人节符号                                       | u+2665 ISOpub | \\2665    | <a href='javascript:alert(&quot;\u2665&quot;)'>\u2665</a> |
| `&diams;`  | ♦     | `&#9830;` | 方块                                                       | u+2666 ISOpub | \\2666    | <a href='javascript:alert(&quot;\u2666&quot;)'>\u2666</a> |

{.show-header}

