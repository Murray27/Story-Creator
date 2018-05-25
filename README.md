# Story-Creator
This uses masm to take in user input an turn it into a short story

comment * «««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««
This program takes user input and output the results in a telling story.
««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««« *

.486                                    ; create 32 bit code
.model flat, stdcall                    ; 32 bit memory model
option casemap :none                    ; case sensitive
include \masm32\include\windows.inc     ; always first
include \masm32\macros\macros.asm       ; MASM support macros

; -----------------------------------------------------------------
; include files that have MASM format prototypes for function calls
; -----------------------------------------------------------------

include \masm32\include\masm32.inc
include \masm32\include\gdi32.inc
include \masm32\include\user32.inc
include \masm32\include\kernel32.inc

; ------------------------------------------------
; Library files that have definitions for function
; exports and tested reliable prebuilt code.
; ------------------------------------------------

includelib \masm32\lib\masm32.lib
includelib \masm32\lib\gdi32.lib
includelib \masm32\lib\user32.lib
includelib \masm32\lib\kernel32.lib

; --------------------------------------------------------------
; This is a prototype for a procedure used in the demo. It tells
; MASM how many parameters are passed to the procedure and how
; big they are. This makes procedure calls far more reliable as
; MASM will not allow different sizes or different numbers of
; parameters to be passed. Note that a C calling convention
; procedure CAN have a variable number of arguments but these
; examples use the normal Windows STDCALL convention which is
; different.
; --------------------------------------------------------------

userName PROTO :DWORD
userAge	PROTO :DWORD
userCity PROTO :DWORD
userCollege PROTO :DWORD
userProfession PROTO :DWORD
userAnimal PROTO :DWORD
userPetName PROTO :DWORD

	
.code                       ; Tell MASM where the code starts

; «««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««
start:                      ; The CODE entry point to the program
call main                   ; branch to the "main" procedure
exit
; «««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««««

main proc
LOCAL txtinput1:DWORD        ; a "handle" for the text returned by "input"
LOCAL txtinput2:DWORD 
LOCAL txtinput3:DWORD 
LOCAL txtinput4:DWORD 
LOCAL txtinput5:DWORD 
LOCAL txtinput6:DWORD 
LOCAL txtinput7:DWORD 

; Introduction

print chr$(13,10,"This program plays a word game which will ask for your input")
print chr$(13,10,"and output a story based on your answers.")
print chr$(13,10,"Please enter the following information:",13,10,13,10,)
    
; Ask for for user input and store in a variable

mov txtinput1, input("	Name: ")		
mov txtinput2, input(13,10,"	Age: ")
mov txtinput3, input(13,10,"	Name of a city: ")
mov txtinput4, input(13,10,"	Name of a College: ")
mov txtinput5, input(13,10,"	A profession: ")
mov txtinput6, input(13,10,"	A type of animal: ")
mov txtinput7, input(13,10,"	A pet's name: ")	

; Prints the story
; txtinput(n) is put into its correct variable

print chr$(13,10,13,10,"    There once was a person named ")
invoke userName, txtinput1
print chr$(" who lived in ")
invoke userCity, txtinput3
print chr$(". At the age of ",13,10,"   ")
invoke userAge, txtinput2
print chr$(", ")
invoke userName, txtinput1
print chr$(" went to college at ")
invoke userCollege, txtinput4
print chr$(". ")
invoke userName, txtinput1
print chr$(" graduated and went to work",13,10,"   as a ")
invoke userProfession, txtinput5
print chr$(". Then, ")
invoke userName, txtinput1
print chr$(" adopted a(n) ")
invoke userAnimal, txtinput6
print chr$(" named ")
invoke userPetName, txtinput7
print chr$(". They",13,10,"	both lived happily ever after!",13,10,13,10)	

ret
main endp

; Gives the direction to the variables

userName proc string:DWORD
print string
ret
userName endp

userAge proc string:DWORD
print string
ret
userAge endp

userCity proc string:DWORD
print string
ret
userCity endp

userCollege proc string:DWORD
print string
ret
userCollege endp

userProfession proc string:DWORD
print string
ret
userProfession endp

userAnimal proc string:DWORD
print string
ret
userAnimal endp

userPetName proc string:DWORD
print string
ret
userPetName endp

end start                       ; Tell MASM where the program ends
