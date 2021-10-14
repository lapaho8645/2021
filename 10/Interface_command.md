
## S6a/S6d (MME-HSS)
#### AIR/AIA (Authentication-Information-Request/Answer)
MME는 가입자를 인증하기 위해 HSS에서 인증 데이터를 요청/반환
#### ULR/ULA (Update-Location-Request/Answer)
MME는 HSS에 자신의 Id를 저장, HSS로부터 가입 데이터를 가져옴
#### NOR/NOA (Notification-Request/Answer)
MME는 HSS에 PDN 주소 및 기타 첨부 정보 저장
#### PUR/PUA (Purge Request/Answer)
MME는 HSS에 UE가 장기간 비활성 상태임을 알림
#### IDR/IDA (Insert-Subscription-Data-Request/Answer)
HSS는 가입 데이터가 변경되었음을 알림
#### DSR/DSA (Delete-Subscriber-Data-Request/Answer)
HSS는 가입 데이터 일부가 삭제되었음을 알림
#### CLR/CLA (Cancel-Location-Request/Answer)
HSS는 가입자 분리를 요청
#### RSR/RSA (Reset-Request/Answer)
HSS는 MME에게 reset을 알리고 데이터를 동기화
## GX (PCRF-PGW)
#### RAR/RAA (Re-Auth-Request/Answer)
네트워크 접속 장치의 가입자 단말의 세션 상태를 확인하여 재인증을 요청
#### CCR/CCA (Credit-Control-Request/Answer)
특정 서비스에 대해 신용 승인을 요청
## Rx (PCRF-AF)
#### AAR/AAA (AA-Request/Answer)
특정 애플리케이션을 수행시키기 위해 요청
#### RAR/RAA (Re-Auth-Request/Answer)
네트워크 접속 장치의 가입자 단말의 세션 상태를 확인하여 재인증을 요청
#### ASR/ASA (Abort-Session-Request/Answer)
비정상적으로 판단되는 가입자 단말을 강제 종료 요청
#### STR/STA (Session-Termination-Request/Answer)
가입자 단말의 서비스 종료를 요청
