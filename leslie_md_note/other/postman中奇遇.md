1. 在postman中 发现了 postman的java 请求 :

   

![postman截图](postman中奇遇.assets/截屏20200526134421png)

​				

```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
Request request = new Request.Builder()
  .url("https://www.neimanmarcus.com/c/beauty-skin-care-lip-treatments-cat64560760?filterOptions=%7B%22Designer%22%3A%5B%5D%2C%22priceBandLower%22%3A%5B%22Under%20%2425%22%5D%2C%22In%20Store%22%3A%5B%5D%7D&navpath=cat000000_cat000285_cat10470738_cat64560760&page=1&source=leftNav")
  .method("GET", null)
  .addHeader("Cookie", "TLTSID=33AF96CC9E39109E254ECD8CE91A8580; TLTUID=33AF96CC9E39109E254ECD8CE91A8580; AGA=17000001:17200001; SPCR=1; dt_favorite_store=\"\"; profile_data=%7B%22firstName%22%3A%22%22%2C%22currencyPreference%22%3A%22HKD%22%2C%22countryPreference%22%3A%22HK%22%2C%22securityStatus%22%3A%22Anonymous%22%2C%22cartItemCount%22%3A0%7D; W2A=3322740746.56665.0000; CChipCookie=2030108682.61525.0000; _pxhd=19b14baabf366dbcd16fe15096953d0a0229f7bee762602334f1326c34f84c8d:335e8b61-9e39-11ea-9029-c3365d56b5b4; DYN_USER_ID=25634018668; DYN_USER_CONFIRM=a529ba9dc77fd78e711204d2258cac35; WID=25634018668; TS01fabb3d=01d3b151d5586be7539963370064e4da022c0f13b10ace333b49ae9060ecde26f1ca715428c3cc4640c0d95e3a00cea0eef48ca125ccafb45cb60f6d8533f1ac239d07456389919537ba4265f8e3dbe5a921c977c318d78e2981d31c773a2be438eefd11f0cba1e6d67f63e598fa75374282749665723a5848025435f5212cf5511d034d1d5fbc947bc3138e112ee3ab6dfdd06434; _cplid=1590379897389622; _optuid=1590379897389527; _optanalytics=\"\"; JSESSIONID=Au79oAcAcobvM7Qqjy3Wy2X1ynGCuDnvh4ndQV8H.jsession; dt_personalize_data=%7B%22lastUpdatedDate%22%3A%22Tue+May+26+00%3A25%3A00+CDT+2020%22%2C%22bestCustomer%22%3A%22n%22%2C%22plcc%22%3A%22n%22%2C%22customerJourneySegment%22%3A%220%22%2C%22inCircleLevel%22%3A%220.0%22%2C%22promos%22%3A%5B%5D%2C%22customerScore%22%3A%220.0%22%2C%22emailSubscriber%22%3A%22n%22%7D; tms_data={DT-2017.03}a3HwxssoiZzaMm5Pj2Bv6L13Gv8Ad/WZkJm2zLBiJ229KIABsN0Vbg/Tmef/T0VV1+0ApCvVZYzpVcNsGQSN27Pl6A2dYuuvtyAC913/ljT/doEZa94mW+S0J3JgPidW1wxNhHXspO7CnHPEKQ8eI1EZvHj72J5KLT5JD5jDSqpHtTqeiaOoEdmgIPjlhrqPEEp/4yrmrba4JbTSNg30M8T8eav6IMTTmGpxOLqPU/rdnPgf9T9WiWVZwdfvyEnlcW+Ca7VIJgUdXyfiO0GihECOpcnbS/PgV/+9MBz28CO7MYzqVCFEVRrl/drpMIqQQ4cShNQYvyeXVLcDLFO9p4v1dk+rnA7gGfULbDizPTA2u7W3FbiRNHCyTYvhe0kzomsB0Cy0TZ0t3CBjKfBjZsqhT49H/5Owy2KFyK80Ckxs6RKGY/Jqoc1+a3bRgyX0gZssqZ+EoRVKI3z9lZRTjGH9PZ4UN4wt/Ww3MvoLJrk7CUplVoIrHsgKrb7cHpCk6rMShHmeB282d04YFtGyOHfn6fsm1ZAJTN752c2kVaVZ7rFm5gDBK+b5p7PUrqXv0kRz0ytx2J9MV7+2pD2zdyIGq9HJgeHGLsSd/vMi+uYaMp3fq5WW9LUKvl7pIXbSJEuwNcsdZNLP89pV3+Op9243Igm9ELEl1fUgHCd+JasrJV9eszuFT3NmMD8nVIaTj8MDTgEHRlG790hJgzS6e7rRt9ZteUpmDbByzQwKd2b1Kvf2szdf/xMNT3bBs172HYL67PbhjgUZN3kuR2LkiJQHGc/DIZQWYXye3vgpfEMu2mzx/t8LeGTHukJvpdL+8up3FOXH0HoFrwFpvVMUpH/OgJOX8pDmoiTrNc5G4z4Qo+tgZjaLsq0VVxP1FRFp8Tqrg4ZQ0027y7KOedgLa9PWBQmn82OFF19lG8DyU+WPncwu7IvFYxmnqzEcxbfJtM4K/dvNsBmvq8oFjQahu9kBOPnUkym3Vv1auR1wEy8B0xnH73zMFgeaTuti/GEN; TS01bbdfeb=01d3b151d5c18f7f1bf72ed359685af403de98a30e27e6e8feba93a9c93548bb3a3b69ae08a0fd4cacca7c8fd532ef85039d705d2ae68144a56e514e7c7c50ad08b04834707f1fc86543dcd4e8245b0fd14b21989ece8088a4539bd68ae7b1be70f87613097d18b24012be2858f129798d14fff357ad5021ddca8223aa54947b4983ca320ff369ce041c169c797403889af0a84c57c8ebc3c3d4a91647fa4b400393cd9822b2d5b26428ec91cd44d80cce396ef34afd3883188b7963f55d1d56f22567db1372ffa848604f9f8a2ea3062844bde2bbb87dd4e7b2665b97da7d48a22c782b6f")
  .build();
Response response = client.newCall(request).execute();
```

1. 感觉请求很 优雅，利于做爬虫，百度了一下 ，基于Apache的  OkHttpCLient。get 到了新技能。
2. [关于okHttpClient的资料](https://www.jianshu.com/p/da4a806e599b) 

