在excel左上角的菜单，点击 “开发工具” - 选“Visual Basic”，在新界面中选 “插入” - “模块”，输入如下代码

```visual basic
Function URLDecode(ByVal strIn)
        URLDecode = ""
        Dim sl: sl = 1
        Dim tl: tl = 1
        Dim key: key = "%"
        Dim kl: kl = Len(key)
        sl = InStr(sl, strIn, key, 1)
        Do While sl > 0
            If (tl = 1 And sl <> 1) Or tl < sl Then
                URLDecode = URLDecode & Mid(strIn, tl, sl - tl)
            End If
            Dim hh, hi, hl
            Dim a
            Select Case UCase(Mid(strIn, sl + kl, 1))
                Case "U" 'Unicode URLEncode
                    a = Mid(strIn, sl + kl + 1, 4)
                    URLDecode = URLDecode & ChrW("&H" & a)
                    sl = sl + 6
                Case "E" 'UTF-8 URLEncode
                    hh = Mid(strIn, sl + kl, 2)
                    a = Int("&H" & hh) 'ascii码
                    If Abs(a) < 128 Then
                        sl = sl + 3
                        URLDecode = URLDecode & Chr(a)
                    Else
                        hi = Mid(strIn, sl + 3 + kl, 2)
                        hl = Mid(strIn, sl + 6 + kl, 2)
                        a = ("&H" & hh And &HF) * 2 ^ 12 Or ("&H" & hi And &H3F) * 2 ^ 6 Or ("&H" & hl And &H3F)
                        If a < 0 Then a = a + 65536
                        URLDecode = URLDecode & ChrW(a)
                        sl = sl + 9
                    End If
                Case Else 'Asc URLEncode
                    hh = Mid(strIn, sl + kl, 2) '高位
                    a = Int("&H" & hh) 'ascii码
                    If Abs(a) < 128 Then
                        sl = sl + 3
                    Else
                        hi = Mid(strIn, sl + 3 + kl, 2) '低位
                        a = Int("&H" & hh & hi) '非ascii码
                        sl = sl + 6
                    End If
                    URLDecode = URLDecode & Chr(a)
            End Select
            tl = sl
            sl = InStr(sl, strIn, key, 1)
        Loop
        URLDecode = URLDecode & Mid(strIn, tl)
    End Function
```

关掉VB窗口，直接在A5单元格输入框输入函数=URLDecode(A1)，就可以得到所要的结果了

如果要把中文编译成编码呢？也是可以的
```visual basic
Function GetURL$(txt$, Optional LC = &H804)     
    Dim a() As Byte: a = StrConv(txt, vbFromUnicode, LC)
    For i = 0 To UBound(a)
        GetURL = GetURL & "%" & Right("0" & Hex(a(i)), 2)
    Next
End Function
```
