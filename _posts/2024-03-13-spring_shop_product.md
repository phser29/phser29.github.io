---
layout: single
title: "spring product"
categories: java
tag: spring_shop
toc: true
---

## 상품등록

- 상품등록 테이블
- 등록 구현 & 위지윅 적용
- jquery ui 위젯 사용

### 카테고리 리스트

- JSON.parse() : 메서드는 JSON 문자열의 구문을 분석하고, 그 결과에서 JavaScript 값이나 객체를 생성

- 라이브러리 추가

```
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-databind</artifactId>
  <version>2.12.1</version>
</dependency>
```

- 카테고리 controller

```
@RequestMapping(value = "/goodsEnroll", method = RequestMethod.GET)
public void goodsEnrollGET(Model model) throws Exception{
	log.info("상품 등록 페이지 접속");
	
	List<CateVO> list = adminService.cateList();
	
	//JSON String 배열로 변환
	ObjectMapper objm = new ObjectMapper();
	String cateList = objm.writeValueAsString(list);
	
	model.addAttribute("cateList", cateList);
}
```

- 카테고리 배열 변수 선언

```
let cateList = JSON.parse('${cateList}');

let cate1Array = new Array();
let cate2Array = new Array();
let cate3Array = new Array();
let cate1Obj = new Object();
let cate2Obj = new Object();
let cate3Obj = new Object();

let cateSelect1 = $(".cate1");		
let cateSelect2 = $(".cate2");
let cateSelect3 = $(".cate3");
```

- 카테고리 배열 해당 클레스에 적용
- 같은 티어끼리 비교 후에 obj에 저장
```
function makeCateArray(obj, array, cateList, tier){
	for(let i = 0; i < cateList.length; i++){
		if(cateList[i].tier === tier){
			obj = new Object();
			
			obj.cateName = cateList[i].cateName;
			obj.cateCode = cateList[i].cateCode;
			obj.cateParent = cateList[i].cateParent;
			
			array.push(obj);
		}
	}
}

//배열 초기화
makeCateArray(cate1Obj,cate1Array,cateList,1);
makeCateArray(cate2Obj,cate2Array,cateList,2);
makeCateArray(cate3Obj,cate3Array,cateList,3);
```

- 대분류
	- 카테고리에서 티어가 1번째 인 것 호출

```
// tier1의 정보 호출
for(let i = 0; i < cate1Array.length; i++){
	cateSelect1.append("<option value='"+cate1Array[i].cateCode+"'>" + cate1Array[i].cateName + "</option>");
}
```

- 중분류
	- 카테고리에서 티어가 2번째 인 것 호출
  - 대분류의 데이터를 기점으로 DB에서 카테고리 코드가 같은 것 출력

```
$(cateSelect1).on("change", function () {
	let selectVal1 = $(this).find("option:selected").val();
	cateSelect2.children().remove();
	cateSelect2.append("<option value='none'>선택</option>");
	
	// 대분류의 cateParent와 일치하는 tier2의 정보 호출
	for(let i=0; i<cate2Array.length; i++) {
		if(selectVal1 === cate2Array[i].cateParent) {
			cateSelect2.append("<option value='"+cate2Array[i].cateCode+"'>" + cate2Array[i].cateName + "</option>");
		}
	}
});
```

- 소분류
  - 중분류의 데이터를 기점으로 DB에서 카테고리 코드가 같은 것 출력

```
$(cateSelect2).on("change", function() {
 	let selectVal2 = $(this).find("option:selected").val();
	cateSelect3.children().remove();
	cateSelect3.append("<option value='none'>선택</option>");
	
	for(let i=0; i<cate3Array.length; i++) {
		if(selectVal2 === cate3Array[i].cateParent) {
			cateSelect3.append("<option value='"+cate3Array[i].cateCode+"'>"+cate3Array[i].cateName+"</option>");
		}
	}
});
```

### 상품 목록 구현



## 상품 이미지 업로드


## 메인화면 네비기능


## 검색 필터링


## 상품 상세 페이지


