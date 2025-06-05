# Chronos API-명세서


## 1. 회원

### 1.1 회원가입
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/signup | POST | 새로운 회원을 등록 |


**요청**
- Body
```json
{
  "email": "user@example.com",
  "password" : "password123",
  "nickname" : "user_nickname"
}
```

**응답**

- Success
```json
{
  "code" : 201,
  "message" : "회원가입에 성공하였습니다."  
}
```

- Error
```json
{
  "code" : 400,
  "message" : "회원가입에 실패하였습니다.",
  "error" : "SIGNUP_FAILED"
}
```

### 1.2 인증 코드 전송
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/email/send | POST | 이메일 인증을 위한 인증 코드 전송 |

**요청**
- Body
```json
{
  "email": "user@example.com"
}
```
**응답**

- Success
```json
{
  "code" : 202,
  "message" : "인증 코드 전송에 성공하였습니다."
}
```

- Error
```json
{
  "code" : 400,
  "message" : "인증 코드 전송에 실패하였습니다.",
  "error" : "EMAIL_SEND_FAILED" 
}
```

### 1.3 인증 코드 확인 
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/email/verification | POST | 전송된 인증 코드 일치 여부 확인 |

**요청**
- Body
```json
{
  "email": "user@example.com",
  "code" : "code1234"
}
```
**응답**

- Success
```json
{
  "code" : 200,
  "message" : "인증에 성공하였습니다."  
}
```

- Error
```json
{
  "code" : 400,
  "message" : "인증에 실패하였습니다.",
  "error" : "EMAIL_VERIFICATION_FAILED"
 
}
```

### 1.4 로그인 
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/login | POST | 회원 로그인 |

**요청**
- Body
```json
{
  "email": "user@example.com",
  "password" : "password123"
}
```
**응답**

- Success
```json
{
  "code" : 200,
  "message" : "로그인에 성공하였습니다."
}
```

- Error
```json
{
  "code" : 400,
  "error" : "LOGIN_FAILED",
  "message" : "로그인에 실패하였습니다."
}
```

### 1.5 내 정보 조회 
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/me | GET | 내 정보 조회 |

**요청**
- Header
  
```  
Authorization: Bearer <JWT_ACCESS_TOKEN>
```

**응답**

- Success 
```json
{
  "code" : 200,
  "message" : "내 정보 조회에 성공하였습니다.",
  "email": "user@example.com",
  "nickname" : "user_nickname"
}
```
  

- Error
```json
{
  "code" : 400,  
  "message" : "내 정보 조회에 실패하였습니다.",
  "error" : "ME_FAILED"
}
```

- 로그인 되어있지 않은 경우
```json
{
  "code" : 401,
  "message" : "로그인이 필요합니다.",  
  "error" : "UNAUTHORIZED"  
}
```
- 토큰이 만료된 경우
```json
{
  "code" : 401,
  "message" : "토큰이 만료되었습니다.",
  "error" : "UNAUTHORIZED"  
}
```

### 1.6 로그아웃
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/logout | POST | 클라이언트에서 JWT 토큰을 삭제하여 로그아웃 처리 |

**요청**
- Header
  
```  
Authorization: Bearer <JWT_ACCESS_TOKEN>
```

**응답**

- Success  
```json
{
  "code" : 200,
  "message" : "로그아웃에 성공하였습니다."
}
```

- 토큰이 만료된 경우
```json
{
  "code" : 401,
  "message" : "토큰이 만료되었습니다.",
  "error" : "UNAUTHORIZED"  
}
```


  ### 1.7 닉네임 변경
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/me/nickname | PATCH | 내 정보 조회 페이지에서 닉네임을 변경 |

**요청**
- Header
  
```  
Authorization: Bearer <JWT_ACCESS_TOKEN>
```
- Body
```json
{
  "nickname" : "user_nickname"
}
```
**응답**

- Success
```json
{
  "code" : 200,
  "message" : "닉네임 변경에 성공하였습니다."
}
```

- Error
```json
{
  "code" : 400,
  "error" : "CHANGE_NICKNAME_FAILED",
  "message" : "닉네임 변경에 실패하였습니다."
}
```

- 토큰이 만료된 경우
```json
{
  "code" : 401,
  "message" : "토큰이 만료되었습니다.",
  "error" : "UNAUTHORIZED"  
}
```


  ### 1.8 비밀번호 변경
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/me/password | PATCH | 내 정보 조회 페이지에서 비밀번호를 변경 |

**요청**
- Header
  
```  
Authorization: Bearer <JWT_ACCESS_TOKEN>
```
- Body
```json
{
  "currentPassword" : "current_password123",
  "newPassword" : "new_password123"
}
```
**응답**

- Success
```json
{
  "code" : 200,
  "message" : "비밀번호 변경에 성공하였습니다."
}
```

- Error
```json
{
  "code" : 400,
  "error" : "CHANGE_PASSWORD_FAILED",
  "message" : "비밀번호 변경에 실패하였습니다."
}
```

- 토큰이 만료된 경우
```json
{
  "code" : 401,
  "message" : "토큰이 만료되었습니다.",
  "error" : "UNAUTHORIZED"  
}
```

  ### 1.9 회원탈퇴
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/members/me | DELETE | 내 정보 조회 페이지에서 회원탈퇴 |

**요청**
- Header
  
```  
Authorization: Bearer <JWT_ACCESS_TOKEN>
```
- Body
```json
{
  "password" : "password123"
}
```
**응답**

- Success
```json
{
  "code" : 200,
  "message" : "회원탈퇴에 성공하였습니다."
}
```

- Error
```json
{
  "code" : 400,
  "error" : "UNREGISTER_FAILED",
  "message" : "회원탈퇴에 실패하였습니다."
}
```

- 토큰이 만료된 경우
```json
{
  "code" : 401,
  "message" : "토큰이 만료되었습니다.",
  "error" : "UNAUTHORIZED"  
}
```

---

## 2. 일정 관리

### 2.1 일정 추가
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/schedules/ | POST | 새로운 일정을 추가 |

**요청**
- Header
```
Authorization: Bearer <JWT_ACCESS_TOKEN>
```
  
- Body
```json
{
  "title" : "schedule_title"
  "description" : "schedule_description"
  "category" : "schedule_category"
  "startAt" : "YYYY-MM-DD HH:MM"
  "endAt" : "YYYY-MM-DD HH:MM"
}
```

**응답**

- Success
```json
{
  "code" : 201,
  "message" : "일정 추가에 성공하였습니다."  
}
```

- Error
```json
{
  "code" : 400,
  "message" : "일정 추가에 실패하였습니다.",
  "error" : "SCHEDULE_ADD_FAILED"
}
```

### 2.2 일정 수정
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/schedules/{scheduleId} | PUT | 등록된 일정을 수정정 |


**요청**
- Header
```
Authorization: Bearer <JWT_ACCESS_TOKEN>
```
  
- Body
```json
{
  "title" : "schedule_title"
  "description" : "schedule_description"
  "category" : "schedule_category"
  "startAt" : "YYYY-MM-DD HH:MM"
  "endAt" : "YYYY-MM-DD HH:MM"
}
```

**응답**

- Success
```json
{
  "code" : 200,
  "message" : "일정 수정에 성공하였습니다."  
}
```

- Error
```json
{
  "code" : 400,
  "message" : "일정 수정에 실패하였습니다.",
  "error" : "SCHEDULE_UPDATE_FAILED"
}
```

### 2.3 일정 삭제
| URI | METHOD | 설명 |
|---------------|------|-------|
| /api/schedules/{scheduleId} | DELETE | 등록된 일정을 삭제 |


**요청**
- Header
```
Authorization: Bearer <JWT_ACCESS_TOKEN>
```  


**응답**

- Success
```json
{
  "code" : 200,
  "message" : "일정 삭제에 성공하였습니다."  
}
```

- Error
```json
{
  "code" : 400,
  "message" : "일정 삭제에 실패하였습니다.",
  "error" : "SCHEDULE_DELETE_FAILED"
}
```



