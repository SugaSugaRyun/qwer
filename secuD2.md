# 싱글벙글 가륜이의 문제풀이 (bof1~4)

<br/>

## __문제 접근__:

> 1. 코드를 읽고 스택의 구조를 파악한다.  
> 스택에는 리턴,SFP,이노센트,버퍼 순으로 있을것이다.
> 2. 버퍼의 주소, 이노센트의 주소를 찾는다.
> 3. 두 주소의 거리를 구하여 버퍼의 시작으로부터 이노센트의 시작거리를 구할 수 있다.
> 4. 위 거리를 d라고 하자, d만큼 버퍼에 쓸모없는 값을 입력하고 4byte크기의 값을 추가하여 bof를 발생시키고 이노센트 값을 조작한다.
> 5. 그후 쉘을 얻을 수 있다.

</br>  

## __구체적 풀이__:

> 1. bof1은 표준입력으로 부터 값을 받는다.  
> (python -c "print 'x'*140 + 'aaaa'";cat) | ./bof1  
> 를 입력하면 된다.
> |(파이프)를 이용하여 표준 입력을 전환하는 방법이다.  
> ()를 이용하여 두가지 명령어를 하나로 묶어준다.  
> 여기서 cat을 이용하는 것은 cat앞의 값이 입력되면 입력스트림이 종료됨과 동시에 프로그램이 종료되기 떄문에 cat을 넣어줌으로써 입력스트림이 계속 열린상태로 있을 수 있도록 하여 쉘을 사용하기 위함이다.  
> bof2.pw : e31a76fc

> 2. bof2는 명령줄인자로 값을 받는다.
> 프로그램을 실행할 때 인자를 전달하여 준다.  
> 임의의 인자를 하나 전달한 후 버퍼와 이노센트의 거리를 구한다. 그후 이노센트 값을 변조한다.  
> ./bof2 \`python -c "print 'x'*140+'aaaa'"`  
> bof3.pw : 78ac9531

> 3. bof3는 표준입력으로 부터 값을 받는다.  
> bof1과 같은 방법으로 풀면된다. 단,   KEY가 'a'이므로 이것에 맞추면 된다.  
> bof4.pw : 64869b0d

> 4. bof4는 명령줄 인자로 답을 받는다.  
> 그래서 입력은 bof2처럼 하면 된다.  
> 하지만 이 문제에서 중요한 것은 이노센트에 어떻게 값을 잘 전달할지이다.  
> 빅엔디안을 따라야 하므로 거꾸로 값을 전달한다. 78, 56, 34, 12  
> 이 값을 4byte로 한번에 보내기 위하여 다음과 같이 작성한다.  
> ./bof4 \`python -c "print 'x'*140+'\x78\x56\x34\x12'"`  
> 이렇게 이어서 작성하는 것이 가장 중요하다!  
> bof5.pw : c75cfe84