---
title: 汇编语言程序设计：用户输入‘1’时显示数字0~9，输入‘2’时显示学号，其他输入时程序退出
tags: []
id: '166'
categories:
  - - 汇编语言
date: 2021-04-25 16:16:08
---

题目具体为：获取用户输入，并根据用户输入的内容显示不同内容。其中，用户输入‘1’时显示数字0~9，输入‘2’时显示学号，其他输入时程序退出。

提示：

INT 21H 功能调用使用说明如下：  
（1）入口：AH＝00H 或AH＝4CH  
功能：程序终止  
（2）入口：AH＝01H  
功能：读键盘输入到AL中并回显  
（3）入口：AH＝02H，DL=数据  
功能：写DL中的数据到显示屏  
（4）入口：AH＝08H  
功能：读键盘输入到AL中无回显  
（5）入口：AH＝09H，DS:DX=字符串首地址，字符串以 '$' 结束  
功能：显示字符串，直到遇到 '$' 为止

以下为源码

```
.MODEL SMALL   
.STACK 16H   
.DATA 
MSE DB 30H,31H,32H,33H,34H,35H,36H,37H,38H,39H,'$'    
NUM DB '202000010001（此处填写自己的学号）',0Dh,0AH,'$'
.CODE   
.STARTUP 
MAIN PROC FAR      
CALL INPUT   
CALL SHOWSTR   
JMP MAIN   
EXIT: MOV AH,4CH    
INT 21H 
MAIN ENDP   

INPUT PROC NEAR    
MOV AH, 08H   
INT 21H   
RET 
INPUT ENDP 
 
SHOWSTR PROC NEAR   
MOV SI, OFFSET  MSE 
CMP AL,31H
JZ STEP1
JNZ STEP2

STEP1: MOV DX,OFFSET MSE
MOV AH ,9
INT 21H
JMP A

STEP2: CMP AL,32H
JZ STEP3
JNZ STEP4
JMP A
STEP3: MOV SI, OFFSET NUM
CMP AL,01H
MOV DX,OFFSET NUM
MOV AH,9
INT 21H
JMP A

STEP4: MOV AH, 00H
INT 21H
JMP A

A: RET   
 
SHOWSTR ENDP  
END 
```