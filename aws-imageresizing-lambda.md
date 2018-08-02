
1. S3버켓 만듬
2. 정책에 익명 접근 가능 추가
3. 스태틱 웹사이트 호스팅 만들고, 호스트 주소 적어놈(다른탭에 잇씀)

4. 람다 펑션 만들고
5. 람다 코드는 이미지 서버 zip 올림
6. 테스트 해보고
환경변수는 2개 설정하는데, BUCKET에 버켓명 URL에 호스트 주소(아까적어둔)
커스텀 정책 만들고 

      {
        "Version": "2012-10-17",
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "logs:CreateLogGroup",
              "logs:CreateLogStream",
              "logs:PutLogEvents"
            ],
            "Resource": "arn:aws:logs:*:*:*"
          },
          {
            "Effect": "Allow",
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::[여기 버킷명]/*"    
          }
        ]
      }
      
  트리거는 API 트리거, 오픈으로, 메모리 1536 타임아웃 10초 추천
  
  그리고 s3에서 리다이렉션 설정함
  
  <RoutingRules>
    <RoutingRule>
        <Condition>
            <KeyPrefixEquals/>
            <HttpErrorCodeReturnedEquals>404</HttpErrorCodeReturnedEquals>
        </Condition>
        <Redirect>
            <Protocol>https</Protocol>
            <HostName>[람다 호스트 주소]</HostName>
            <ReplaceKeyPrefixWith>prod/resize?key=</ReplaceKeyPrefixWith>
            <HttpRedirectCode>307</HttpRedirectCode>
        </Redirect>
    </RoutingRule>
</RoutingRules>
