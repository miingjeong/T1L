docs.oracle.com/cd/E26925_01/html/E25888/user-8.html

 

 

 
Kerberos 티켓 관리 - Oracle Solaris 관리: 보안 서비스

Kerberos 티켓 관리 이 절에서는 티켓 획득, 확인 및 삭제 방법에 대해 설명합니다. 티켓에 대한 개요는 Kerberos 서비스의 작동 방식을 참조하십시오. 티켓의 이점 SEAM 릴리스 또는 Oracle Solaris 릴리스

docs.oracle.com
docs.oracle.com/cd/E26925_01/html/E25888/intro-5.html#scrolltocKerberos 서비스란?
 
Kerberos 서비스란? - Oracle Solaris 관리: 보안 서비스

Kerberos 서비스란? Kerberos 서비스는 네트워크를 통해 보안 트랜잭션을 제공하는 클라이언트-서버 구조입니다. 이 서비스는 무결성 및 프라이버시를 비롯하여 강력한 사용자 인증을 제공합니다.

docs.oracle.com
Kerberos 서비스는 네트워크를 통해 보안 트랜잭션을 제공하는 클라이언트-서버 구조입니다. 이 서비스는 무결성 및 프라이버시를 비롯하여 강력한 사용자 인증을 제공합니다. 인증은 네트워크 트랜잭션의 송신인과 수신자가 맞는지 보증합니다. 이 서비스는 또한 앞뒤로 전달되는 데이터의 유효성을 확인(무결성)하고 전송 중 데이터를 암호화합니다(프라이버시). Kerberos 서비스를 사용할 경우 다른 시스템에 로그인, 명령 실행, 데이터 교환 및 안전한 파일 전송 등이 가능합니다. 또한 이 서비스는 관리자가 서비스 및 시스템에 대한 액세스를 제한할 수 있도록 해주는 인증 서비스를 제공합니다. 또한 Kerberos 사용자는 다른 사용자가 자신의 계정에 액세스하는 것을 규제할 수 있습니다.

Kerberos 서비스는 단일 사인 온(SSO) 시스템이므로, 세션당 한 번만 서비스에 대해 자신을 인증하기만 하면 됩니다. 그러면 세션 동안의 이후 모든 트랜잭션이 자동으로 보안 처리됩니다. 서비스에 대해 인증을 받은 후에는 Kerberos 기반 명령(예: ftp 또는 rsh)을 사용할 때마다 인증하거나, NFS 파일 시스템의 데이터에 액세스할 필요가 없습니다. 따라서 네트워크를 통해 암호를 전송할 경우 암호가 인터셉트될 가능성이 있는데, 이 서비스를 사용할 때마다 이러한 방식으로 암호를 전송할 필요가 없습니다.

Oracle Solaris 릴리스의 Kerberos 서비스는 MIT(Massachusetts Institute of Technology)에서 개발한 Kerberos V5 네트워크 인증 프로토콜을 기반으로 합니다. Kerberos V5 제품을 사용해 본 적이 있는 사용자라면 Oracle Solaris 버전을 매우 친숙하게 찾을 수 있을 것입니다. Kerberos V5 프로토콜은 사실상 네트워크 보안을 위한 산업 표준이기 때문에 Oracle Solaris 버전에서는 다른 시스템과의 상호 운용성이 향상됩니다. 즉, Oracle Solaris 릴리스의 Kerberos 서비스는 Kerberos V5 프로토콜을 사용하는 시스템에서 작동하기 때문에 이기종 네트워크를 통해서도 보안 트랜잭션이 가능합니다. 또한 이 서비스는 도메인 간에 그리고 단일 서비스 내에서 인증과 보안을 제공합니다.

Kerberos 서비스는 Oracle Solaris 응용 프로그램을 실행하는 데 있어 유연성을 제공합니다. 네트워크 서비스(예: NFS 서비스, telnet, ftp)에 대해 Kerberos 기반 요청 및 Kerberos 기반이 아닌 요청을 모두 허용하도록 서비스를 구성할 수 있습니다. 그러면 Kerberos 서비스가 사용으로 설정되지 않은 시스템에서 현재 응용 프로그램이 실행 중이더라도 계속 작동합니다. 물론 Kerberos 기반 네트워크만 허용하도록 Kerberos 서비스를 구성할 수도 있습니다.

Kerberos 서비스가 제공하는 보안 방식은 GSS-API(Generic Security Service Application Programming Interface)를 사용하는 응용 프로그램을 사용할 경우 인증, 무결성 및 프라이버시를 위해 Kerberos 사용을 허용합니다. 그러나 다른 보안 방식이 개발된 경우 응용 프로그램이 Kerberos 서비스를 계속 사용할 필요는 없습니다. 이 서비스는 모듈 방식으로 GSS-API에 통합되었으므로 GSS-API를 사용하는 응용 프로그램이 필요에 가장 적합한 보안 방식을 사용할 수 있습니다.

 

klist :

만들어진 티켓 목록을 확인
klist -l 로 모든 티켓 목록을 확인 가능
klist -vA 로 모든 티켓 상세내용을 확인 가능 (macOS : klist -vA, linux : klist -aA)
[출처] kerberos 명령어|작성자 Curycu

kinit : 

kerberos ticket 생성
kinit -p your_principal 형태로 default realm 외 티켓 생성이 가능 (principal 예시 : your_id@your_realm)
kinit -t your_keytab 형태로 keytab을 이용한 티켓 생성이 가능
[출처] kerberos 명령어|작성자 Curycu

 
Curycu's Box : 네이버 블로그

https://www.facebook.com/Curycu

blog.naver.com
m.blog.naver.com/PostView.nhn?blogId=diadbtmd&logNo=220062932863&proxyReferer=https:%2F%2Fwww.google.com%2F

 
리눅스 diff 와 patch

diif 사용법 diff는 말 그대로 difference, 차이를 만들어 주는 프로그램입니다. 차이는 디렉토리간일 수 ...

blog.naver.com
diif

 

사용법

diff는 말 그대로 difference, 차이를 만들어 주는 프로그램입니다.

차이는 디렉토리간일 수 도 있고 파일일 수도 있습니다. 두 가지 모두 지원합니다.

 

예를 들어 수정할 소스가 있습니다. 그럼 복사를 해서 원본파일은 변경하지 않습니다.

$cp –a test test.orig

이렇게 되면

test/

test.orig/

test.orig는 원본이므로 변경하지 않고 test에서 변경을 합니다.

수정 후 무엇이 바뀌었는지 알기가 힘듭니다.

이때 diff를 사용합니다.

$diff –urN test.orig test > test.diff

 

이렇게 하면 diff 프로그램이 두 디렉토리를 탐색하면서 같은 이름끼리 비교를 한 뒤 차이를

test.diff에 기록합니다.

 

옵션

옵션은 –u 옵션은 "unified format"으로 diff포맷을 지정할 때 사용합니다. –c 옵션은 "context format"으로 u옵션으로 사용할 때와 c옵션을 사용할 때의 결과를 보면 차이를 알 수 있습니다.

 

-r 옵션은 경로를 지정한 디렉토리 안의 서브 디렉토리를 전부 거슬로 들어가면서(recursive) 안에 있는 파일을 전부 비교하라는 뜻입니다. 이것을 지정하지 않으면 명령행에서 지정한 디렉토리만 비교합니다.

 

-N옵션은 새 파일도 diff에 포함하라는 뜻입니다. 자신이 고친 디렉토리에 새로 만들은 파일이 있을 경우 꼭 사용해야 합니다.

 

patch

 

사용법

실제 만들어진 패치(위에서 diff를 한 파일이 패치파일)를 적용하는 방법은 아래와 같습니다.

$patch –p0 < test.diff

patch는 항상 표준 입력으로부터 입력을 받습니다.

 

 

옵션

-p 옵션은 주어진 패치의 경로에서 몇 단계를 올라갈지 입니다. –p0 이면 여기에서 하라는 의미입니다. 쉽게 말해서 패치를 어디서부터 적용할 것인가 입니다.

 

$patch [옵션] [원본 파일] [패치파일]

$patch –p1 < ../패치할 파일이 있는 디렉토리/

$patch –p2 < ./패치할 파일이 있는 디렉토리/

diff : 차이를 만등러 주는 프로그램

ㅍㅐ치 

 

 

 

ls 옵션

ttend.tistory.com/765