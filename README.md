# Okul-Projesi-Database-Tasarimi
#Egitim Projemdeki SQL Odevim 


Users tablosu, okulla ilişkili her türden kişi için genel bilgileri içerir. (Students, Teachers, Principals etc.)
1) [Id]: Her kullanıcıya benzersiz bir kimlik (UserID) atanır. 
2) [Name]         : Bu alanda ilgili kullanıcının ad ve soyad bilgileri tutulur.
3) [Email]        : Bu alanda kullanıcının e-posta adresi tutulur.
4) [PhoneNumber]  : Bu alanda kullanıcının telefon numarası tutulur.

``` SQL
CREATE TABLE [dbo].[Users](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](50) NOT NULL,
	[Email] [varchar](50) NOT NULL,
	[PhoneNumber] [varchar](20) NOT NULL,
 CONSTRAINT [PK_Users] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

Students tablosu, öğrencilere ait detayları içerir.
1) [UserId]             : Users tablosu ile UserId alanı üzerinden ilişkilendirilir.
2) [ParentsContactInfo] : Öğrencinin velisinin iletişim bilgileri tutulur.
3) [ClassId]            : Kayıtlı olduğu sınıfın ID'si burada tutulur.
4) [DepartmentId]       : Öğrencinin kayıtlı olduğu bölümün kimliği tutulur. 

```SQL 
CREATE TABLE [dbo].[Students](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[UserId] [int] NOT NULL,
	[ParentsContactInfo] [varchar](100) NOT NULL,
	[ClassId] [int] NOT NULL,
	[DepartmentId] [int] NOT NULL,
 CONSTRAINT [PK_Students] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

Courses tablosu, derslere ait detayları içerir.
1) [Id]        : Her bir ders kaydına benzersiz bir kimlik (UserID) atanır. 
2) [Name]      : Dersin adını saklamak için kullanılır.
3) [TeacherId] : Dersin atanmış olduğu öğretmenin kimliğini saklamak için kullanılır.

```SQL 
CREATE TABLE [dbo].[Courses](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](100) NOT NULL,
	[TeacherId] [int] NOT NULL,
 CONSTRAINT [PK_Courses] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
````
ExamTypes tablosu, sınav türlerini/aşamalarını içerir.
1) [Id]           : Her bir sınav türüne benzersiz bir kimlik (UserID) atanır. 
2) [ExamTypeName] : Sınav türlerinin adlarını saklamak için kullanılır.
   
````SQL
CREATE TABLE [dbo].[ExamTypes](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[ExamTypeName] [varchar](50) NOT NULL,
 CONSTRAINT [PK_ExamTypes] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
`````

Exams tablosu, yapılan sınavların bilgilerini içerir.
1) [Id]          : Her bir sınav için benzersiz bir kimlik atanır.
2) [CoursesId]   : Sınavın hangi dersle ilişkili olduğunu belirtmek için kullanılır.
3) [ExamDate]    : Sınavın tarihini saklamak için kullanılır.
4) [ExamTypesId] : Sınavın hangi türde olduğunu belirtmek için kullanılır. 
 
````SQL
CREATE TABLE [dbo].[Exams](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[CoursesId] [int] NOT NULL,
	[ExamDate] [date] NOT NULL,
	[ExamTypesId] [int] NOT NULL,
 CONSTRAINT [PK_Exams] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
````
ExamResults tablosu, yapılan sınavların sonuçlarını içerir.
1) [Id]        : Her bir sınav sonucu için benzersiz bir kimlik atanır.
2) [StudentId] : Sınav sonucunun hangi öğrenciye ait olduğunu belirtmek için kullanılır.
3) [ExamId]    : Sınav sonucunun hangi sınava ait olduğunu belirtmek için kullanılır.
4) [Grade]     : Öğrencinin aldığı notu saklamak için kullanılır.

```SQL
CREATE TABLE [dbo].[ExamResults](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[StudentId] [int] NOT NULL,
	[ExamId] [int] NOT NULL,
	[Grade] [int] NOT NULL,
 CONSTRAINT [PK_ExamResults] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```
Classes tablosu,  okuldaki sınıfların adını içerir.(Hazırlık, Sınıf1 etc)
1) [Id]   : Her bir sınıf için benzersiz bir kimlik atamak için kullanılır.
2) [Name] : Sınıfın adını saklamak için kullanılır. 

```SQL
CREATE TABLE [dbo].[Classes](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](100) NOT NULL,
 CONSTRAINT [PK_Classes] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

Departments tablosu, okuldaki bölümlerin adını içerir.
1) [Id]   : Her bir bölüm için benzersiz bir kimlik atamak için kullanılır.
2) [Name] : Bölümün adını saklamak için kullanılır.


```SQL
CREATE TABLE [dbo].[Departments](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](100) NOT NULL,
 CONSTRAINT [PK_Departments] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```



```SQL
CREATE TABLE [dbo].[StudentTranscripts](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[StudentId] [int] NOT NULL,
	[CourseId] [int] NOT NULL,
	[MidtermGrade] [int] NOT NULL,
	[FinalGrade] [int] NOT NULL,
	[OverallGrade] [float] NOT NULL,
 CONSTRAINT [PK_StudentTranscripts] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```
