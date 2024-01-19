the decompiled main()
```c
int main(int argc,char **argv)

{
  bool bVar1;
  int iVar2;
  int local_10;
  int i;
  
  if (argc == 2) {
    local_10 = 0;
    for (i = 0; argv[1][i] != '\0'; i = i + 1) {
      local_10 = local_10 + argv[1][i];
    }
    if ((i == 0x10) && (local_10 == 0x6e2)) {
      bVar1 = true;
    }
    else {
      bVar1 = false;
    }
    if (bVar1) {
      printf("Yes, %s is correct!\n",argv[1]);
      iVar2 = 0;
    }
    else {
      printf("No, %s is not correct.\n",argv[1]);
      iVar2 = 1;
    }
  }
  else {
    puts("Must provide one argument.");
    iVar2 = -1;
  }
  return iVar2;
}
```

From the first if condition we gather the password must be 0x10 characters long (16)

we need a password with 10 characters where the sum of its characters is 0x6e2 (1762)

with this python script to help
```python
payload = "nnnnnnnnnnnnnnnp"
c = 0
for i in payload:
    c = c + ord(i) 
print(c)
```

```sh
┌──(kali㉿lahabrea)-[~/Downloads/crackmes]
└─$ p3 4.py
1762


┌──(kali㉿lahabrea)-[~/Downloads/crackmes]
└─$ ./crackme4 nnnnnnnnnnnnnnnp
Yes, nnnnnnnnnnnnnnnp is correct!
```

