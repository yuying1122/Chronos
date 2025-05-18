# Chronos API-명세서


## 1. 회원

### 1.1 회원가입
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/signup | POST | 새로운 회원을 등록 |

**요청**
```json
{
  "email": "이메일(String)",
  "password" : "비밀번호(String)",
  "nickname" : "회원 닉네임(String)"
}
```

**응답**

- SUCCESS
```json
{
  "message" : "회원가입에 성공하였습니다."  
}
```

- ERROR
```json
{
  "error" : "SIGNUP_FAILED",
  "message" : "회원가입에 실하였습니다."
  "code" : 400
}
```

### 1.2 인증 코드 전송
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/email/send | POST | 이메일 인증을 위한 인증 코드 전송 |

**요청**
```json
{
  "email": "이메일(String)"
}
```
**응답**

- SUCCESS
```json
{
  "message" : "인증 코드 전송에 성공하였습니다."
}
```

- ERROR
```json
{
  "error" : "CODE_SEND_FAILED"
  "message" : "인증 코드 전송에 실패하였습니다."
  "code" : 400
}
```

### 1.3 인증 코드 확인 
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/email/verification | POST | 전송된 인증 코드 일치 여부 확인 |

**요청**
```json
{
  "email": "이메일(String)",
  "code" : "인증코드(String)"
}
```
**응답**

- SUCCESS
```json
{
  "message" : "인증에 성공하였습니다."  
}
```

- ERROR
```json
{
  "error" : "CODE_VERIFICATION_FAILED",
  "message" : "인증에 실패하였습니다."
}
```

### 1.4 로그인 
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/login | POST | 회원 로그인 |

**요청**
```json
{
  "email": "이메일(String)",
  "password" : "비밀번호(String)"
}
```
**응답**

- SUCCESS
```json
{
  "message" : "로그인에 성공하였습니다."
}
```

- ERROR
```json
{
  "error" : "LOGIN_FAILED",
  "message" : "로그인에 실패하였습니다."
}
```

### 1.5 내 정보 조회 
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/me | GET | 내 정보 조회 |

**요청**

**응답**

- SUCCESS

- ERROR
```json
{
  "message" : "내 정보 조회에 실패하였습니다."
}
```

**예외**

- 로그인 되어있지 않은 경우
```json
{
  "error" : "UNAUTHORIZED"
  "message" : "로그인이 필요합니다."
  "code" : 401
}
```
- 토큰이 만료된 경우
```json
{
  "error" : "UNAUTHORIZED"
  "message" : "토큰이 만료되었습니다."
  "code" : 401
}
```



