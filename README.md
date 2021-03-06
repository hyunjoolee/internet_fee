<!DOCTYPE html>
<html lang="en">
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"><title>Tables</title>
	<script src="./internet_fee.js"></script>
<style>
/* Select */
.custom-select {
  position: relative;
  font-family: Arial;
}

.custom-select select {
  display: none; /*hide original SELECT element:*/
}

.select-selected {
  background-color: DodgerBlue;
}

/*style the arrow inside the select element:*/
.select-selected:after {
  position: absolute;
  content: "";
  top: 14px;
  right: 10px;
  width: 0;
  height: 0;
  border: 6px solid transparent;
  border-color: #fff transparent transparent transparent;
}

/*point the arrow upwards when the select box is open (active):*/
.select-selected.select-arrow-active:after {
  border-color: transparent transparent #fff transparent;
  top: 7px;
}

/*style the items (options), including the selected item:*/
.select-items div,.select-selected {
  color: #ffffff;
  padding: 8px 16px;
  border: 1px solid transparent;
  border-color: transparent transparent rgba(0, 0, 0, 0.1) transparent;
  cursor: pointer;
  user-select: none;
}

/*style items (options):*/
.select-items {
  position: absolute;
  background-color: DodgerBlue;
  top: 100%;
  left: 0;
  right: 0;
  z-index: 99;
}

/*hide the items when the select box is closed:*/
.select-hide {
  display: none;
}

.select-items div:hover, .same-as-selected {
  background-color: rgba(0, 0, 0, 0.1);
}

/* button */
.dropbtn {
  background-color: #4CAF50;
  color: white;
  padding: 10px;
  font-size: 16px;
  border: none;
}

.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f1f1f1;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1;
}

.dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

.dropdown-content a:hover {background-color: #ddd;}
.dropdown:hover .dropdown-content {display: block;}
.dropdown:hover .dropbtn {background-color: #3e8e41;}

/* 테이블 스타일 */
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg .tg-0lax{text-align:left;vertical-align:top}
</style>
</head>

<script type="text/javascript">

window.onload = pageLoad;
function pageLoad(){
	select_changed();
};
	
function get_values() {
	var ret = {
            speed:0,
            num:0,
            contract:0,
			addition:0,
			fee1:0,
			device1:0,
			phonenum1:0,
			fee2:0,
			device2:0,
			phonenum2:0,
			phonenum2:0,
			tv:0,
			numtv:0
        };
	var selected = document.getElementById("speed");
	ret.speed = selected.options[selected.selectedIndex].value;
	
	var selected = document.getElementById("num");
	ret.num = selected.options[selected.selectedIndex].value;
	
	var selected = document.getElementById("contract");
	ret.contract = selected.options[selected.selectedIndex].value;
	
	var selected = document.getElementById("addition");
	ret.addition = selected.options[selected.selectedIndex].value;
	
	var selected = document.getElementById("fee1");
	ret.fee1 = selected.options[selected.selectedIndex].value;
	
	var selected = document.getElementById("device1");
	ret.device1 = selected.options[selected.selectedIndex].value;
	
	var selected = document.getElementById("phonenum1");
	ret.phonenum1 = selected.options[selected.selectedIndex].value;
	
	var selected = document.getElementById("fee2");
	ret.fee2 = selected.options[selected.selectedIndex].value;
	
	var selected = document.getElementById("device2");
	ret.device2 = selected.options[selected.selectedIndex].value;
	
	var selected = document.getElementById("phonenum2");
	ret.phonenum2 = selected.options[selected.selectedIndex].value;
	
	var selected = document.getElementById("tv");
	ret.tv = selected.options[selected.selectedIndex].value;
	
	var selected = document.getElementById("numtv");
	ret.numtv = selected.options[selected.selectedIndex].value;
	
	return ret;
}

// 선택값 변경될 때마다 호출
function select_changed() {
	var v = get_values()
	
	var array1 = [ // 요금 테이블 [100MB, 500MB, 1GB]
		[ 39000, 49000, 59000 ], // 무약정
		[ 39000, 49000, 59000 ], // 1년
		[ 39000, 49000, 59000 ], // 2년 
		[ 39000, 49000, 59000 ], // 3년
		[ 39000, 49000, 59000 ], // 결합
	];
	var array2 = [ // 약정 할인 테이블
		[ 0,     0,     0     ], // 무약정
		[ 8000,  6000,  7000  ], // 1년
		[ 13000, 13200, 16000 ], // 2년
		[ 19000, 21000, 24000 ], // 3년
		[ 19000, 21000, 24000 ], // 결합
	];	
	var array3 = [ // 결합 할인 테이블
		[ 0,     0,     0     ], // 무약정
		[ 0,     0,     0     ], // 1년
		[ 0,     0,     0     ], // 2년
		[ 0,     0,     0     ], // 3년
		[ 0,     5000,  5000  ], // 결합
	];
	var array4 = [ 5000, 9000, 10000, 12000 ]; // 추가결합할인
	
	var array5 = [ // 전화 요금 테이블 [고급형C, 일반형]
		[ 2000, 5000 ], // 무약정
		[ 2000, 5000 ], // 1년
		[ 2000, 5000 ], // 2년
		[ 2000, 5000 ], // 3년
		[ 2000, 5000 ], // 결합
	];
	
	var array6 = [ // 전화 할인금액 테이블 [고급형C, 일반형]
		[ 1000, 0    ], // 무약정
		[ 1000, 1000 ], // 1년
		[ 1000, 1500 ], // 2년
		[ 1000, 2000 ], // 3년
		[ 1000, 2000 ], // 결합
	];
	
	var array7 = [ // TV 요금 테이블 [보급형, 일반형, 고급형]
		[ 12000, 15000, 19000 ], // 무약정
		[ 12000, 15000, 19000 ], // 1년
		[ 12000, 15000, 19000 ], // 2년
		[ 12000, 15000, 19000 ], // 3년
		[ 12000, 15000, 19000 ], // 결합
	];
	
	var array8 = [ // TV 할인금액 테이블 [보급형, 일반형, 고급형]
		[ 0   , 0   , 0    ], // 무약정
		[ 1500, 1500, 1500 ], // 1년
		[ 3500, 3500, 3500 ], // 2년
		[ 5000, 5000, 5000 ], // 3년
		[ 5000, 5000, 5000 ], // 결합
	];
	
	var array9 = [ // 전화단말기 테이블 [IP455, IP450, WPI8800, CPG402ON]
		[ 99000, 102000, 105000, 36000 ], // 무약정
		[ 69000, 72000,  75000,  36000 ], // 1년
		[ 69000, 72000,  75000,  36000 ], // 2년
		[ 60000, 70000,  75000,  36000 ], // 3년
		[ 30000, 35000,  40000,  36000 ], // 결합
	];
	
	var array10 = [ // 전화 매월 납입금액 테이블 [IP455, IP450, WPI8800, CPG402ON]
		[ 99000, 89000, 105000, 36000 ], // 무약정
		[ 5750,  4910,  6250,   1000  ], // 1년
		[ 2880,  2460,  3120,   1000  ], // 2년
		[ 1660,  1380,  2080,   1000  ], // 3년
		[ 830,   550,   1110,   1000  ], // 결합
	];
	
	var array11 = [ // 모바일 결합 테이블 [12000, 14900, 19000]
		[ 0   , 0   , 0    ], // 1
		[ 1500, 1500, 1500 ], // 2
		[ 3500, 3500, 3500 ], // 3
		[ 5000, 5000, 5000 ], // 4~10
	];
	
	var aone   = array1[v.contract][v.speed] * v.num;
	var atwo   = array2[v.contract][v.speed] * v.num;
	var athree = array3[v.contract][v.speed] * v.num;
	var afour  = array4[v.addition];
	var afive  = parseInt((aone - atwo - athree - afour) * 0.07);
	var asix   = aone - atwo - athree - afour - afive
	document.getElementById('a_one').innerHTML   = aone;
	document.getElementById('a_two').innerHTML   = atwo;
	document.getElementById('a_three').innerHTML = athree;
	document.getElementById('a_four').innerHTML  = afour;
	document.getElementById('a_five').innerHTML  = afive;
	document.getElementById('a_six').innerHTML   = asix;
	
	var bone   = (array5[v.contract][v.fee1] * v.phonenum1) + (array5[v.contract][v.fee2] * v.phonenum2)
	var btwo   = (array6[v.contract][v.fee1] * v.phonenum1) + (array6[v.contract][v.fee2] * v.phonenum2)
	var bthree = (array10[v.contract][v.fee1] * v.phonenum1)+ (array10[v.contract][v.fee2] * v.phonenum2)
	var bfour  = bone - btwo + bthree
	document.getElementById('b_one').innerHTML   = bone;
	document.getElementById('b_two').innerHTML   = btwo;
	document.getElementById('b_three').innerHTML = bthree;
	document.getElementById('b_four').innerHTML  = bfour;
	
	var cone   = array7[v.contract][v.tv] * v.numtv
	var ctwo   = array8[v.contract][v.tv] * v.numtv
	var cthree = parseInt((cone - ctwo) * 0.07);
	var cfour  = v.numtv * 4000;
	var cfive  = cone - ctwo - cthree + cfour;
	document.getElementById('c_one').innerHTML   = cone;
	document.getElementById('c_two').innerHTML   = ctwo;
	document.getElementById('c_three').innerHTML = cthree;
	document.getElementById('c_four').innerHTML  = cfour;
	document.getElementById('c_five').innerHTML  = cfive;
	
	
	document.getElementById('g_one').innerHTML   = aone + bone + cone;
	document.getElementById('g_two').innerHTML   = atwo + athree + afour + afive + btwo + ctwo + cthree;
	document.getElementById('g_three').innerHTML = asix + bfour + cfive;
}
/*
 var internet_speed_changed = function (select_obj){
	// 우선 selectbox에서 선택된 index를 찾고 
	var selected_index = select_obj.selectedIndex;
	// 선택된 index의 value를 찾고 
	var selected_value = select_obj.options[selected_index].value;
	// 원하는 동작을 수행한다. 여기서는 그냥 alert해주는 식으로만 처리함. 
	alert(selected_value);
	*/


</script>

<body>

<h3>■ 요금셋팅 (입력구간)</h3>
<table class="tg">
  <tr>
    <th class="tg-0lax" style="text-align:center;width:150px;">인터넷속도</th>
    <th class="tg-0lax" style="text-align:center;width:150px;">인터넷수</th>
    <th class="tg-0lax" style="text-align:center;width:150px;">약정</th>
    <th class="tg-0lax" style="text-align:center;width:200px;">추가결합할인 <br> <가무사> <가끼모> <참가결></th>
    <th class="tg-0lax" style="text-align:center;width:150px;">7%할인</th>
  </tr>
  <tr>
    <td class="tg-0lax">
		<select id="speed" onchange="select_changed()" style="text-align:center;width:130px;">
			<option value="0">100MB</option>
			<option value="1">500MB</option>
			<option value="2">1GB</option>
		</select>
	</td>
    <td class="tg-0lax">
		<select id="num" onchange="select_changed()" style="width:100px;">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
		</select>
	</td>
    <td class="tg-0lax">
		<select id="contract" onchange="select_changed()" style="width:100px;">
			<option value="0">무약정</option>
			<option value="1">1년</option>
			<option value="2">2년</option>
			<option value="3">3년</option>
			<option value="4">결합</option>
		</select>
	</td>
    <td class="tg-0lax">
		<select id="addition" onchange="select_changed()" style="width:100px;">
			<option value="0">5000</option>
			<option value="1">9000</option>
			<option value="2">10000</option>
			<option value="3">12000</option>
		</select>
	</td>
    <td class="tg-0lax">7%</td>
  </tr>
</table>
<br>
<table class="tg">
  <tr>
    <th class="tg-0lax" style="text-align:center;width:150px;">인터넷/전화<br>요금제</th>
    <th class="tg-0lax" style="text-align:center;width:150px;">단말기명</th>
    <th class="tg-0lax" style="text-align:center;width:150px;">전화댓수</th>
    <th class="tg-0lax" style="text-align:center;width:200px;">인터넷 전화 요금제</th>
    <th class="tg-0lax" style="text-align:center;width:150px;">단말기명</th>
    <th class="tg-0lax" style="text-align:center;width:150px;">전화댓수</th>
	<th class="tg-0lax" style="text-align:center;width:150px;">TV요금제</th>
	<th class="tg-0lax" style="text-align:center;width:150px;">TV댓수</th>
	<th class="tg-0lax" style="text-align:center;width:150px;">7%할인</th>
  </tr>
  <tr>
    <td class="tg-0lax">
		<select id="fee1" onchange="select_changed()" style="width:100px;">
			<option value="0">일반형</option>
			<option value="1">고급형C</option>
		</select>
	</td>
    <td class="tg-0lax">
		<select id="device1" onchange="select_changed()" style="width:100px;">
			<option value="0">IP445</option>
			<option value="1">IP450</option>
			<option value="2">WPI8800</option>
			<option value="3">CPG402ON</option>
		</select>
	</td>
    <td class="tg-0lax">
		<select id="phonenum1" onchange="select_changed()" style="width:100px;">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
			<option value="4">4</option>
			<option value="5">5</option>
		</select>
	</td>
    <td class="tg-0lax">
		<select id="fee2" onchange="select_changed()" style="width:100px;">
			<option value="0">일반형</option>
			<option value="1">고급형C</option>
		</select>
	</td>
    <td class="tg-0lax">
		<select id="device2" onchange="select_changed()" style="width:100px;">
			<option value="0">IP445</option>
			<option value="1">IP450</option>
			<option value="2">WPI8800</option>
			<option value="3">CPG402ON</option>
		</select>
	</td>
    <td class="tg-0lax">
		<select id="phonenum2" onchange="select_changed()" style="width:100px;">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
			<option value="4">4</option>
			<option value="5">5</option>
		</select>
	</td>
	<td class="tg-0lax">
		<select id="tv" onchange="select_changed()" style="width:100px;">
			<option value="0">보급형</option>
			<option value="1">일반형</option>
			<option value="2">고급형</option>
		</select>
	</td>
	<td class="tg-0lax">
		<select id="numtv" onchange="select_changed()" style="width:100px;">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
		</select>
	</td>
	<td class="tg-0lax">7%</td>
  </tr>
</table>

<h3>■ 인터넷요금</h3>
<table class="tg">
  <tr>
    <th class="tg-ne9s" colspan="11" style="text-align:center;">인터넷</th>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align:center;width:150px;">인터넷요금</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">약정할인</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">결합할인</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">추가결합할인</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">7% 할인</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">최종 납부 금액</td>
  </tr>
  <tr>
    <td class="tg-0lax"><span id="a_one"></span></td>
    <td class="tg-0lax"><span id="a_two"></td>
    <td class="tg-0lax"><span id="a_three"></span></td>
    <td class="tg-0lax"><span id="a_four"></span></td>
    <td class="tg-0lax"><span id="a_five"></span></td>
    <td class="tg-0lax"><span id="a_six"></span></td>
  </tr>
</table>
<br>
<table class="tg">
  <tr>
    <th class="tg-ne9s" colspan="11" style="text-align:center;">전화</th>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align:center;width:150px;">전화요금</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">약정/결합할인</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">단말기할부금+임대료</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">최종 납부 금액</td>
  </tr>
  <tr>
    <td class="tg-0lax"><span id="b_one"></span></td>
    <td class="tg-0lax"><span id="b_two"></td>
    <td class="tg-0lax"><span id="b_three"></span></td>
    <td class="tg-0lax"><span id="b_four"></span></td>
  </tr>
</table>
<br>
<table class="tg">
  <tr>
    <th class="tg-ne9s" colspan="11" style="text-align:center;">TV</th>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align:center;width:150px;">TV요금</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">약정/결합할인</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">7% 할인</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">셋탑이용료</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">최종 납부 금액</td>
  </tr>
  <tr>
    <td class="tg-0lax"><span id="c_one"></span></td>
    <td class="tg-0lax"><span id="c_two"></td>
    <td class="tg-0lax"><span id="c_three"></span></td>
    <td class="tg-0lax"><span id="c_four"></span></td>
    <td class="tg-0lax"><span id="c_five"></span></td>
  </tr>
</table>


<h3>■ 약정기간 총 할인</h3>
<table class="tg">
  <tr>
    <th class="tg-ne9s" colspan="11" style="text-align:center;">인터넷</th>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align:center;width:150px;">약정할인</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">결합할인</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">추가결합할인</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">7% 할인</td>
  </tr>
  <tr>
    <td class="tg-0lax"><span id="d_one"></span></td>
    <td class="tg-0lax"><span id="d_two"></td>
    <td class="tg-0lax"><span id="d_three"></span></td>
    <td class="tg-0lax"><span id="d_four"></span></td>
  </tr>
</table>
<br>
<table class="tg">
  <tr>
    <th class="tg-ne9s" colspan="11" style="text-align:center;">전화 / TV</th>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align:center;width:150px;">약정/결합할인</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">약정/결합할인</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">7% 할인</td>
  </tr>
  <tr>
    <td class="tg-0lax"><span id="e_one"></span></td>
    <td class="tg-0lax"><span id="e_two"></td>
    <td class="tg-0lax"><span id="e_three"></span></td>
  </tr>
</table>
<br>
<table class="tg">
  <tr>
    <th class="tg-ne9s" colspan="11" style="text-align:center;">최종</th>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align:center;width:150px;">총할인</td>
  </tr>
  <tr>
    <td class="tg-0lax"><span id="f_fee"></span></td>
  </tr>
</table>
<h3>■ 최종</h3>
<table class="tg">
  <tr>
    <th class="tg-ne9s" colspan="11" style="text-align:center;">최종</th>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align:center;width:150px;">할인전금액</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">총할인</td>
    <td class="tg-0lax" style="text-align:center;width:150px;">납부금액</td>
  </tr>
  <tr>
    <td class="tg-0lax"><span id="g_one"></span></td>
    <td class="tg-0lax"><span id="g_two"></td>
    <td class="tg-0lax"><span id="g_three"></span></td>
  </tr>
</table>
</body>


</html>

