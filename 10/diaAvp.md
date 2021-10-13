## Grouped AVP Values
데이터 필드가 실제로 AVP의 시퀀스임을 의미
## 3GPP TS 29.215
http://www.arib.or.jp/english/html/overview/doc/STD-T63V12_20/5_Appendix/Rel13/29/29215-d70.pdf
## S9 specific Diameter AVPs
![image](https://user-images.githubusercontent.com/64197428/137098750-23a4388f-99a8-40cb-adcb-6007ad3af817.png)
#### Subsession-Id
The Subsession-Id AVP (AVP code 2202) is of type Unsigned32, and it is used to uniquely identify a subsession within the S9 session. The Subsession-Id AVP shall be selected by the V-PCRF.
#### Subsession-Operation
The Subsession-Operation AVP (AVP code 2203) is of type of Enumerated, and it indicates the operation to be performed on the subsession.
The following values are defined:
> TERMINATION (0)
> This value is used to indicate that a subsession is being terminated.

> ESTABLISHMENT (1)
> This value is used to indicate that a new subsession is being established.

> MODIFICATION (2)
> This value is used to indicate that an existing subsession is being modified
#### Subsession-Enforcement-Info
