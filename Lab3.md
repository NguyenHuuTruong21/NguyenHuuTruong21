# Lab 3: Indentify context elements

  # 1. Sybsystem context diagrams
    
    Hệ thông con của PrintService, ProjectManagementDatabase subsystems.

    Biểu đồ ngữ cảnh của hệ thống con PrintService:
    
![PlantText](https://www.planttext.com/api/plantuml/png/b55BYi904DtNASfUwS8Bp48oID25IaZc0atobCPEfwUx5SAGayrYZZHNi3K1Fo3eMxvFFQhg__SlyK6wSAWrZIfibG7dwVphSxDOfLngwJsHbULUxi0YSye4Bk2EgeJW7-A8g_rHbvulp40C_XxsB6IoBRIouycDi8E1am4vREE27xIEEg9eTutMHUi3QfvEP_VZFrZa-3x01uvE7mUBDo9z7o_wUjKOGMbjTTC2Jt8br14zZ-fQkSpNqiHpkPTYmvg2A86fuXjE0000__y30000)


     Biểu đồ ngữ cảnh của hệ thống con ProjectManagementDatabase subsystems    
![PlantText](https://www.planttext.com/api/plantuml/png/Z95F3i5G48VtSuhnLYnSm4883H94YWECTZIbVUMzqQGH9xDm95TGKV-JChl9z_jzivZpyTIoGaPsSGGLdvUXPdITpgmzxWqTz2Ao5c13tfe2HZKnoOezmH7fV8zP2tP9Q46M5Uu1ytcMozDaiU1FVAU5wZO1In6yuchj1LbA-PiTu00meSmaKJJDh72CzNgpv5e3bSlR7LkvXt2Wbuc2juhvRPblV19-IAv8GT_zk--oc93JJmEqMFlvWou0003__mC0)



  # 2. Analysis class to design element map
    Ánh xạ các lớp phân tích đến các phần tử thiết kế
    
    Analysis Class      |  Design Element
    ____________________|______________________
    Employee            ||  EmployeeDTO, EmployeeService
    PayrollSystem       ||  Controller Class
    PrintService        ||  Service Class
    HRManager           ||  HRManager
    Report              ||  ReportGenerator, ReportDTO 


    Ánh xạ các lớp phân tích đến các phần tử thiết kế
    
    Analysis Class      |  Design Element
    ____________________|______________________
    Project Data        ||  Project Data
    PayrollSystem       ||  PayrollSystem
    Project Manager     ||  Project Manager
    HRManager           ||  HRManager
    Report              ||  Report

##

  # 3. Design element to owning package map
    Ánh xạ các phần tử thiết kế vào các gói

     Design Element     |  "Owning" Package
    ____________________|______________________
    Employee            ||  Applications: Employee Activities
    PayrollSystem       ||  Middleware::Security:GUI Framework
    PrintService        ||  Service Class
    HRManager           ||  Applications: HRManager


    Ánh xạ các phần tử thiết kế vào các gói

     Design Element     |  "Owning" Package
    ____________________|______________________
    Project Data        ||  Middleware::Security:GUI Framework
    PayrollSystem       ||  Applications: PayrollSystem
    Project Manager     ||  Middleware::Security:GUI Framework
    HRManager           ||  Applications: HRManager

# 4. Architectural layers and their dependencies

![PlantText](https://www.planttext.com/api/plantuml/png/R59BQiCm4Dth54Fs8VikIam_YI41az1LoMAGXrH4bined61AJzP5ZzGhL8qLQhlMRdWVlJVCz-VNCWYoD9LLDUeJ7WbcMLrRer6CTm4ss1BFu5r1VAzFLMrzImIP5dCsOYWSEcIzswABSavpWIrxQ_Tj4AeEwaFz-MzDMLgw8DF8VK-wOIDjibYzvF3CMD75ysbeiIS-6ptM5soS92XvxAZsBB0YHupY-MepMGFcy_jU1BY3hCWNMIDlv2IjG_LgTlnXnYYAyuvSIJ7AKOssCF55j5zaMbC8yE2THBBg4QxyGQkekNNFtTdVOerYJEeUKH3Mw4hRHHl0LyM_PKLL6WWwCAXbRFTxBZy0003__mC0)
