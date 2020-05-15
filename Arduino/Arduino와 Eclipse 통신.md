# Arduino와 Eclipse 통신

## 시리얼 통신

1. `CommPortIdentifier`를 포트의 유효성과 통신가능 상태인지 점검

2. `CommPortIdentifier`의 `open`메서드를 이용해서 시리얼 통신을 할 수 있는 준비상태로 세팅

   => 시리얼 통신을 하기 위해 필요한 포트객체(`CommPort`)가 리턴

3. `CommPort`는 종류가 2가지

   * Serial
   * Paralel

   : CAN통신은 Serial 통신, 아두이노와 라떼판다도 Serial 통신

   => 각 상황에 맞는 `CommPort`객체를 얻어야 작업할 수 있다.

4. `CommPort`를 `SerialPort`로 casting

5. `SerialPort`객체의 `setSerialPortParams`메서드를 이용해서 Serial통신을 위한 기본내용을 설정

   ```java
   serialPort.setSerialPortParams(9600, --> Serial port의 통신속도
   							SerialPort.DATABITS_8, --> 전송하는 데이터의 길이
   							SerialPort.STOPBITS_1, --> stop bit에 설정
   							SerialPort.PARITY_NONE); --> PARITY비트를 사용하지 않겠다고 설정
   ```

   ```markdown
   * PARITY : 오류를 검증하기 위한 비트
   ```

   => Serial포트를 open하고 설정을 잡아놓은 상태

   => 전달되는 데이터(data frame)을 받을 수 있는 상태

6. 데이터를 주고 받을 수 있도록 SerialPort객체에서 Input/Output 스트림을 얻는다.

   => 바이트 단위(io클래스 관점)로 데이터가 송수신되므로 Reader, Writer계열의 스트림을 사용할 수 없고 `InputStream`, `OutputStream` 객체를 사용해야 한다. 

   시리얼포트객체.getInputStream();

   시리얼포트객체.getOutputStream();

7. 데이터 수신과 송신에 대한 처리 

   1.  쓰레드로 처리
   2. 이벤트에 반응하도록 처리

