---
layout: post
title: How I got fired up about programming 
comments: True
summary: The VBA script that got me hooked to coding back in 2006. This is a fun story to read and probably some of you programmers out there recognize the iniial spark of passion for the craft. Enjoy!
tags: [memories, Excel, VBA, Spain]
---

I just tried to figure out where the passion for coding started and I can find two anchors:

* an early affinity / passion for automating tasks (back when studying business economics)

* [an Excel game](http://juegosexcel.com/foro/viewtopic.php?t=6396) that nobody seemed to solve manually back at the day when I was working as a Financial Analyst. Automating that game taught me my first programming skills in VBA and gave me a tremendous empowerment what programming could do.

Since then almost no day goes by where I get stoked about coding and automating boring tasks, making life of others (and myself) easier. When prepared to learn, practice and fail, it has great awards.

The game was about guessing 52 Spanish cities by photo:

![That funny game that was sent around in '06]({{ site.baseurl }}/assets/spanish_cities_start.png)

It’s funny that program took me quite a while to write, probably due to the need to select cells and input guesses until match (Excel specific). Code below (respect for the newby ;) - I would now document it, split it into multiple functions, name variables appropriately, etc.). I don’t have MS Excel anymore, so I can't try it now. The game is still [out there](http://juegosexcel.com/descargas/?did=280) (feel free to try it out and if so please share in the comments ...)

It is basic stuff, you can write a loop in loop solution in Python in minutes, I also note I got so much more routine since then, it's all practice!  

However for me this was a pivotal moment where I brought together a. a need (OK a game, but still people were really bugged by not finding the solution), b. learn to code, and c. a specific context (has to work in Excel, make a button to launch it etc.) - very important: the theory only teaches you so much. 

Since then the best learning has been working on concrete problems and don’t be afraid to make mistakes.

Here is the result: it prefilling all 52 fields with solutions in seconds (I felt so proud of my first ‘real’ script and people's jaw dropping haha):

![Resolved in seconds with the VBA macro]({{ site.baseurl }}/assets/spanish_cities_done.png)

---

It was then that I definitely knew this was MY THING.

---

Disclaimer: sloppy VBA code:

    Sub answers() 

      Sheets(1).Select

      Dim var As Variant, i As Byte, k As Byte, _
      array1 As Variant, array2 As Variant

        array1 = Array("b29", "b39", "b49", "b59", "b69", "b79", "b89", _ 
        "b99", "b109", "b119", "b129", "b139", "b149", "e29", "e39", "e49", _
        "e59", "e69", "e79", "e89", "e99", "e109", "e119", "e129", "e139", _ 
        "e149", "h29", "h39", "h49", "h59", "h69", "h79", "h89", "h99", "h109", _
        "h119", "h129", "h139", "h149", "k29", "k39", "k49", "k59", "k69", "k79", _ 
        "k89", "k99", "k109", "k119", "k129", "k139", "k149")
        
        array2 = Array("ALAVA", "ALBACETE", "ALICANTE", "ALMERIA", "ASTURIAS", "AVILA", _ 
        "BADAJOZ", "BARCELONA", "BILBAO", "BURGOS", "CACERES", "CADIZ", "CANTABRIA", _
        "CASTELLON", "CEUTA", "CIUDAD REAL", "CORDOBA", "CUENCA", "GERONA", "GRANADA", _ 
        "GUADALAJARA", "GUIPUZCOA", "HUELVA", "HUESCA", "JAEN", "LA CORUÑA", "LA RIOJA", _
        "LAS PALMAS", "LEON", "LERIDA", "LUGO", "MADRID", "MALAGA", "MELILLA", "MURCIA", _ 
        "NAVARRA", "ORENSE", "PALENCIA", "MALLORCA", "PAMPLONA", "PONTEVEDRA", "SALAMANCA", _
        "SANTA CRUZ DE TENERIFE", "SANTANDER", "SEGOVIA", "SEVILLA", "SORIA", "TARRAGONA", _ 
        "TENERIFE", "TERUEL", "TOLEDO", "VALENCIA", "VALLADOLID", "VIZCAYA", "ZAMORA", _
        "ZARAGOZA", "VITORIA", "SAN SEBASTIAN", "OVIEDO", "LOGROÑO") 
        
      For i = LBound(array1) To UBound(array1)
          
        For k = 0 To UBound(array2)
        Range(array1(i)).Value = array2(k)
          If Range(array1(i)).Offset(1, 1).Value = "CORRECTO!" Then
            Exit For 
          End If
        Next k

      Next i

    End Sub


---

Enjoy coding :)

If you have a similar experience of where it all started, please use the comments below ...
