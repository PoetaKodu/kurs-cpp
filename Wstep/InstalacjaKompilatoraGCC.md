# [Wstęp](Wstep.md) > Instalacja kompilatora GCC
### <div align="right">Kurs C++ `by Poeta Kodu`</div>

GCC (ang. *GNU Compiler Collection*) to jeden z najpopularniejszych kompilatorów języka (między innymi) C++. Na systemie Windows najlepiej jest go pobrać w paczce, która nazywa się `MinGW-w64`. Po wpisaniu tej frazy w wyszukiwarce internetowej, znajdziesz link do witryny `sourceforge.net`. Następnie, po przejściu do zakładki `Files`, na dole będziesz mógł znaleźć listę dostępnych wersji tej paczki.

![Dostępne wersje paczki MinGW-w64][img mingw-versions]

Możemy zauważyć w jej nazwie wersję kompilatora GCC - generalnie im nowszy, tym lepiej. Pobierz tą, zatytułowaną `x86_64-posix-seh`. Na 32 bitowych systemach operacyjnych może ona nie działać i wtedy można spróbować skorzystać z wersji `-sjlj`. Najlepszym rozwiązaniem będzie i tak przeniesienie się na 64 bitowy system operacyjny.

<!-- Next and previous lesson -->
<hr>
<p>
	Poprzednia lekcja:<br>
	<a href="AbsolutnePodstawy.md">&lt;&lt;&lt; Wstęp &gt; Absolutne podstawy</a>
</p>

<!-- Links and images -->
[img mingw-versions]: Images/MinGWVersions.png