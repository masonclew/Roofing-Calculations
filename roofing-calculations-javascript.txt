//user inputs what shape the roof face is
onEvent("startbutton", "click", function( ) {
  var roofface = getProperty("shapedrop", "value");
  if (roofface == "triangle") {
    setScreen("trianglescreen");
    
  } else if (roofface == "rectangle") {
    setScreen("rectanglescreen");
  } else {
    setScreen("trapeziodscreen");
  }
});
//rectangle area calculations
function rectarea(){
  // user inputs the dimensions (ft)
  var length = getText("lengthinput");
  var width = getText("widthinput");
  return (length*width);
}
//trapeziod area calculations
function traparea(){
  // user inputs the dimensions (ft)
  var short = getText("shortside");
  var long = getText("longside");
  var height = getText("trapheight");
  return((short+long)*(0.5)*(height));
}
//triangle area calculations
function areaoverall() {
  // user inputs the dimensions (ft)
  var triside0 = getText("triside0");
  var triside1 = getText("triside1");
  var triside2 = getText("triside2");
  var sidelist = [];
  // side lengths converted to integers for simplicity
  function makeinteger(){
    triside0 = parseInt(triside0);
    triside1 = parseInt(triside1);
    triside2 = parseInt(triside2);
  }
  // side lengths added to list (used later for perimeter calculations)
  // if statement used to check all inputs are positive
  function addtolist() {
    if (triside0 <= 0 || triside1 <= 0 || triside2 <= 0) {
      setText("finalcost", "invalid dimensions");
    } else {
      appendItem(sidelist,triside0);
      appendItem(sidelist,triside1);
      appendItem(sidelist,triside2);
    }
  }
  //calculates perimeter by looping through the list,
  // and adding every index to the variable total
  function addemup(){
    var total = 0;
    for (var i = 0; i<3; i++){
      total = total + sidelist[i];
    }
    return total;
  }
  makeinteger();
  (addtolist(triside0,triside1,triside2));
  function sp() {
    return (addemup()/2);
  }
  // triangle area calculations (compatible with scalene triangles)
  function calcarea() {
    return Math.sqrt(sp()*(sp()-triside0)*(sp()-triside1)*(sp()-triside2));
  }
  return calcarea();
}
//user clicks desired surface prompting cost/time estimate output in text box
onEvent("calcasp", "click", function( ) {
  setText("finalcost","The cost is roughly" + " $"+Math.round(areaoverall()*3.50)+ 
  "."+ response(areaoverall()));
});
onEvent("calctile", "click", function( ) {
  setText("finalcost","The cost is roughly" + " $"+Math.round(areaoverall()*10.50) + "."+ response(areaoverall()));
});
onEvent("calcmetal", "click", function( ) {
  setText("finalcost","The cost is roughly" + " $"+Math.round(areaoverall()*7.50)+ "."+ response(areaoverall()));
});
onEvent("calcasp1", "click", function( ) {
  setText("finalcost1","The cost is roughly" + " $"+Math.round(rectarea()*3.50) + "."+ response(rectarea()));
});
onEvent("calctile1", "click", function( ) {
  setText("finalcost1","The cost is roughly" + " $"+Math.round(rectarea()*10.50)+ "."+ response(rectarea()));
});
onEvent("calcmetal1", "click", function( ) {
  setText("finalcost1","The cost is roughly" + " $"+Math.round(rectarea()*7.50) + "."+ response(rectarea()));
});
onEvent("calcasp2", "click", function( ) {
  setText("finalcost2","The cost is roughly" + " $"+Math.round(traparea()*3.50)+ "." + response(traparea()));
});
onEvent("calctile2", "click", function( ) {
  setText("finalcost2","The cost is roughly" + " $"+Math.round(traparea()*10.50)+ "." + response(traparea()));
});
onEvent("calcmetal2", "click", function( ) {
  setText("finalcost2","The cost is roughly" + " $"+Math.round(traparea()*7.50) + "."+ response(traparea()));
});
onEvent("back1", "click", function ( ) {
setScreen("homescreen");
});
onEvent("back2", "click", function ( ) {
setScreen("homescreen");
});
onEvent("back3", "click", function ( ) {
setScreen("homescreen");
});
function response(x) {
  //x represents area
  // my list commentary contains various time estimates
  var commentary = [" The replacment should take 2-4 days", 
  " The replacement should take 4-7 days.", 
  " The replacement should take a week",
  " The replacement should take 7-9 days",
  " This roof is huge and will take forever to replace."];
  if (x < 100) {
  return commentary[0];
  } else if (x < 400) {
    return commentary[1];
  } else if (x < 600) {
    return commentary[2];
  } else if (x<1000) {
    return commentary[3];
  } else {
    return commentary[4];
  }

}

