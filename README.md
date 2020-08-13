# 수강신청 프로젝트

기능 : 로그인, 수강 조회, 수강 신청 삽입, 삭제, 수정

환경 : Eclipse JSP, Oracle

●	RDB schema
1)	student(s_id: varchar2, s_pwd: varchar2, s_name: varchar2, s_addr varchar2)

CREATE TABLE student(
s_id varchar2(7) CONSTRAINT student_pk PRIMARY KEY, 
s_pwd varchar2(20) CONSTRAINT student_nn NOT NULL, 
s_name varchar2(6), 
s_addr varchar2(60)
);

2)	course(c_id: varchar2, c_no: number, c_year: number, c_semester: number, c_name: varchar2, c_credit: number, c_max: number, c_time: number, c_where: varchar2)

CREATE TABLE course(
c_id varchar2(8), 
c_no NUMBER, 
c_year NUMBER, 
c_semester NUMBER, 
c_name varchar2(50), 
c_credit NUMBER, 
c_max NUMBER, 
c_time NUMBER, 
c_where varchar2(20), 
CONSTRAINT course_pk PRIMARY KEY(c_id, c_no, c_year, c_semester)
);

3)	enroll(e_sid: varchar2, e_cid: varchar2, e_cno: number, e_year: number, e_semester: number)

CREATE TABLE enroll(
e_sid varchar2(7),
e_cid varchar2(8), 
e_cno NUMBER, 
e_year NUMBER, 
e_semester NUMBER, 
CONSTRAINT enroll_pk PRIMARY KEY(e_sid, e_cid),
CONSTRAINT enroll_fk_student FOREIGN KEY(e_sid) REFERENCES student(s_id), 
CONSTRAINT enroll_fk_teach FOREIGN KEY(e_cid, e_cno, e_year, e_semester) REFERENCES course(c_id, c_no, c_year, c_semester)
);

