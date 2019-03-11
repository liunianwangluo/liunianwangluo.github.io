---
title: windows逆向笔记（三）
date: 2019-03-12 00:34:00
tags: [windows逆向]
---

### pushad,popad,mov
**pushad**：备份现场，将8个寄存器压到堆栈内（EAX,ECX,EDX,EBX,ESP,EBP,ESI和EDI）    
**popad**：还原现场，将堆栈的值弹出给8个寄存器（EAX,ECX,EDX,EBX,ESP,EBP,ESI和EDI）   
**mov**：赋值。mov eax,ecx => 将ecx的值赋给eax，要注意赋值与被赋值的位数要相同，32位赋给32位 
