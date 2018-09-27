package com.jcloud.demo;

import com.jcloud.search.SearchManager;

import org.junit.Test;

public class TestSearchAPI {

// SearchManager构造需要传入的用户对应的appKey和secretKey

SearchManager searchManager = new SearchManager(

"your appKey", "your secretKey");

//*/*

/* 关键词搜索服务

/*/

@Test

public void testSearch() {

try {

String response = searchManager.search("app_name", "数据测试", "app_id",

"", "", "", null, 1, 20, "", "", "a");

System.out.println(response);

}

catch (Throwable throwable) {

throwable.printStackTrace();

}

}

//*/*

/* 数据上报

/*/

@Test

public void testUpload() {

try {

System.out.println(searchManager.dataUpload("app_id", "app_name", "user",

"[{\"cmd\":\"add\",\"fields\":{\"userid\": \"123\", \"cid\": \"123\"," +

"\"imei\": 123,\"action_type\": \"view\", \"action_num\": \"12\"," +

"\"email\": \"123@jd.com\", \"action_detail\": \"123\"}}]"));

}

catch (Exception e) {

e.printStackTrace();

}

}

//*/*

/* 自动补全

/*/

@Test

public void testSuggest(){

try{

String response = searchManager.suggest("app_name","a",1,"","","","");

System.out.println(response);

}

catch (Throwable throwable) {

throwable.printStackTrace();

}

}

//*/*

/* 相关搜索服务请求

/*/

@Test

public void testRelate(){

try{

String response = searchManager.relate("app_name","a",1,"","","","");

System.out.println(response);

}

catch (Throwable throwable) {

throwable.printStackTrace();

}

}

//*/*

/* 热门搜索词

/*/

@Test

public void testHotQueries(){

try{

String response = searchManager.hotqueries("app_name","a","","",0,10,"a");

System.out.println(response);

}

catch (Throwable throwable) {

throwable.printStackTrace();

}

}

}