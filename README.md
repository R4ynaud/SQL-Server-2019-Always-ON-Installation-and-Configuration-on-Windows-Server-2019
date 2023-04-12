# SQL-Server-2019-Always-On-Installation-&-Configuration-on-Windows-Server-2019

![image](https://user-images.githubusercontent.com/93924485/230014292-886f202b-4011-4b76-bddd-4037dfba9dbf.png)


### SQL Server Always On Nedir, Ne İşe Yarar ?


• SQL Server Always On, yüksek kullanılabilirlik (high availability) ve felaket kurtarma (disaster recovery) özellikleri sağlayan bir SQL Server mimarisidir. Bu mimari, birden fazla SQL Server veritabanı örneğinin birbirleriyle senkronize olarak çalışmasına olanak tanır ve böylece bir sunucunun veya veritabanının arızalanması durumunda veri kaybı olmadan çalışmaya devam edebilir.

• Always On, temel olarak iki farklı özellikten oluşur: Always On Failover Cluster Instances (FCI) ve Always On Availability Groups (AG). FCI, birden fazla sunucunun aynı veritabanını paylaştığı ve bir sunucunun arızalanması durumunda diğer sunucunun devraldığı bir yüksek kullanılabilirlik özelliğidir. AG ise, birden fazla sunucunun aynı veritabanlarının farklı kopyalarını senkronize olarak tuttuğu ve bir sunucunun arızalanması durumunda diğer sunucunun veritabanını devraldığı bir yedekleme özelliğidir.

• Always On mimarisi, SQL Server 2012 sürümünden itibaren kullanılabilir hale gelmiştir ve günümüzde SQL Server 2019 sürümünde de kullanılmaktadır. Always On, büyük ölçekli kurumsal veri tabanları için ideal bir çözüm sağlar ve veri kaybını en aza indirerek iş sürekliliği sağlar.


### What Is an SQL Server Always On ?

• SQL Server Always On is a SQL Server architecture that provides high availability and disaster recovery features. This architecture allows multiple SQL Server database instances to work synchronized with each other, so that they can continue to work without data loss in case of server or database failure.

• Always On consists of two different features: Always On Failover Cluster Instances (FCI) and Always On Availability Groups (AG). FCI is a high availability feature where multiple servers share the same database and one server takes over in case of server failure. AG is a backup feature where multiple servers keep different copies of the same databases synchronized and one server takes over in case of database failure.

• Always On architecture has been available since SQL Server 2012 and is still used in SQL Server 2019. Always On provides an ideal solution for large-scale enterprise databases and ensures business continuity by minimizing data loss.





### 1-) Node1 isimli sunucumuzda Server Manager konsolumuzu açarak öncelikle Failover Clustering rolümüzü kurmak için Add Roles and Features linkine tıklayalım.
###     Let's open the Server Manager console on our server named Node1 and click on the "Add Roles and Features" link to install our Failover Clustering role first.


![image](https://user-images.githubusercontent.com/93924485/230022852-82285bb4-37c4-4fe1-9122-19f4e8bdd770.png)


### 2-) Açılan ekranımızda iki seçeneğimiz yer almaktadır.

• Role-based or feature-based insallation : Rol ve Özellik bazında ekleme kurulum yapma imkânı verir. Windows Server 2019 içerisinde sahip olduğumuz sürüme göre, içerisinde bulunan ve ihtiyacımız olan rol ve özellikleri buradan ekleyip kaldırabilmekteyiz.

• Remote Desktop Services installation: Eski zamanlarda Terminal Servis olarak anılan ve şimdi RDS (Remote Desktop Services) uzak masaüstü yapılandırmasını hızlı ve standart olarak buradan yapabilmekteyiz.

• Bu nedenle biz Failover Clustering özelliğini kuracak olduğumuz için Role-based or feature-based insallation seçimini yaparak Next ile ilerliyoruz.


### In our opened screen, we have two options:

• Role-based or feature-based installation: It allows us to add and remove the required roles and features based on our version of Windows Server 2019.

• Remote Desktop Services installation: We can quickly and standardly configure the Remote Desktop Services (formerly known as Terminal Services) from here.

• Therefore, since we will install the Failover Clustering feature, we select the Role-based or feature-based installation option and proceed with Next.


![image](https://user-images.githubusercontent.com/93924485/230023862-8431f9ee-c40c-43fe-bb17-254fc1de2043.png)


### 3-) Biz bir rol kurmayacağımız için özellik ekleme ekranı olan bir sonraki ekrana Next ile ilerliyoruz.
###     We will not create a role, so we proceed to the next screen with an "Next" button which has the feature addition screen. 


![image](https://user-images.githubusercontent.com/93924485/230314059-64198d29-0b9d-4ea5-b6c1-f11624ef1941.png)


### 4-) Özellik ekleme ekranında Failover Clustering özelliğini eklemek için seçelim.
###     Let's select the Failover Clustering feature to add on the feature addition screen.


![image](https://user-images.githubusercontent.com/93924485/230314452-d2253253-16c3-403b-9010-7d6488cd618e.png)


### 5-) Bu özellik ekleme işlemi sırasında yeniden başlatma gerekir ise bunun otomatik olarak gerçekleşmesi için "Restart the destination server automatically if requred" seçimini işaretleyebiliriz. Ben gerekmesi durumunda bunu manuel olarak yapacağım için kurulum adımlarını başlatıp tamamlamak için Install butonuna tıklıyorum.
###     We can select "Restart the destination server automatically if required" option if a restart is needed during the feature addition process to be done automatically. However, if you prefer to do this manually, you can start and complete the installation steps by clicking on the "Install" button.


![image](https://user-images.githubusercontent.com/93924485/230314919-0976ac8d-6bde-42a3-987a-950abb21c33a.png)


### 6-) "Failover Cluster Manager" konsolumuzu açabiliriz.
###     Sure, we can open the "Failover Cluster Manager console".


![image](https://user-images.githubusercontent.com/93924485/230316080-db9d30ac-6fa0-4102-a9a8-ce408927dfb3.png)


### 7-) Konsolumuz açıldı. Bu sunucumuz üzerinde buraya kadar olan işlemlerimiz tamamlandı. Aynı işlemleri diğer sunucularımız üzerinde gerçekleştireceğiz.
###     Great! The console is now open. We have completed the necessary steps on this server. We can now proceed to perform the same steps on our other servers.


![image](https://user-images.githubusercontent.com/93924485/230316504-5b7cafe3-7d5b-44e8-808c-5cf0a6f99abb.png)


### 8-) Cluster kurulumuna geçmeden önce tüm sunucularda "Active Directory Domain Services" kurulumu yapmamız gerekiyor, bunun için aşağıdaki adımları uygulayabilirsiniz. 
###     Before proceeding with the cluster installation, we need to install "Active Directory Domain Services" on all servers. You can follow the steps below for this.


![image](https://user-images.githubusercontent.com/93924485/230349109-c569340b-3547-4379-bea9-393a670a7654.png)


![image](https://user-images.githubusercontent.com/93924485/230349195-c09e5283-a68a-4719-a0f9-07579abce9fe.png)


![image](https://user-images.githubusercontent.com/93924485/230349250-e8d94379-bc64-426d-9d37-727bdc05b926.png)


![image](https://user-images.githubusercontent.com/93924485/230349424-83cc46d0-5abc-4120-8973-334035e0bd12.png)


![image](https://user-images.githubusercontent.com/93924485/230349784-df7cde45-2142-4ab0-8113-bf6219ba6133.png)


![image](https://user-images.githubusercontent.com/93924485/230349852-5aa5515f-fec3-45be-9d18-f463e436a7d2.png)


![image](https://user-images.githubusercontent.com/93924485/230349945-2b0ed18f-2a6e-404e-9405-e0196ad8ace9.png)


![image](https://user-images.githubusercontent.com/93924485/230350058-0d86690f-50ec-435f-bcae-4c7c47afb148.png)


### 9-) Biraz bekledikten sonra kurulum sorunsuz bir şekilde tamamlandı.Bu kısımda “Promote this server to a a domain controller” seçeneği seçip ikinci aşama geçebilirsiniz ve ya Server Manager’i açıp bayrak işareti olan yerden aynı kısma ulaşabilirsiniz.
###     After waiting for a while, the installation was completed successfully. In this step, you can select the "Promote this server to a domain controller" option and proceed to the second step, or you can open the Server Manager and navigate to the same section with the flag icon.


![image](https://user-images.githubusercontent.com/93924485/230354809-a0105db0-5f1a-4e4e-a7d1-b8b271b5d337.png)


### 10-) Add a new forest: Yeni bir Domain yapısı kurulumu yapılır.
Biz ilk defa ortamımıza bir domain yapısı kuracağımız için “Add a new forest” seçeneği ile devam ediyoruz. Aynı ekranda root domain ismi belirlememiz gerekmektedir. Domain adı belirlerken dikkat etmemiz gereken bir kaç husus vardır. Domain adından sonra .(NOKTA)koyularak bir Suffix belirtmemiz gerekmektedir.local,com vb. gibi aksi halde ilerleyemeyiz. Genelde .local şeklinde kurulmaktadır.
###     Add a new forest: This is used to set up a new domain structure.

As we are setting up a domain structure for the first time, we will proceed with the "Add a new forest" option. In the same screen, we need to specify the root domain name. There are a few things we need to consider when choosing a domain name. We need to add a suffix by putting a period (.) after the domain name, such as .local, .com, etc. Otherwise, we cannot proceed. Generally, it is set up as .local.


![image](https://user-images.githubusercontent.com/93924485/230355355-3a4d5ef0-8f2d-43ae-a94e-f5da6bbd9316.png)


### 11-) DSRM şifresi belirleyelim.
###      Let's set the DSRM (Directory Services Restore Mode) password.


![image](https://user-images.githubusercontent.com/93924485/230355953-08dfc05f-a8f3-415f-b59a-3268414e394a.png)


### 12-) DNS Options kısmında bir uyarı çıkıyor.Bu uyarı herhangi bir problem teşkil etmemektedir.Yapımızda bir DNS Server olmadığı  ve DNS Zone üzerinde herhangi bir Delegasyon ataması yapılmadığı için vermektedir.“NEXT” ile devam ediyorum.
###      There is a warning in the DNS Options section. This warning does not pose any problems. It is displayed because there is no DNS Server in our structure and no delegation is assigned on the DNS Zone. I will proceed by clicking "NEXT".


![image](https://user-images.githubusercontent.com/93924485/230356397-a6be4510-89b1-483d-a014-5eccc2cfc2a1.png)


### 13-) Addition Options kısmında domain yapısı için otomatik olarak oluşan NETBIOS name ismini görüyoruz.(NETBIOS yerel ağ üzerindeki farklı bilgisayarların birbiriyle iletişim kurmasını sağlayan bir sistemdir.) “NEXT” ile devam ediyoruz.
###      In the Addition Options section, we see the NETBIOS name that is automatically generated for the domain structure. (NETBIOS is a system that enables different computers on the local network to communicate with each other.) We will proceed by clicking "NEXT".


![image](https://user-images.githubusercontent.com/93924485/230356958-5deec787-a72e-4b11-9a38-b3a732febb7c.png)


### 14-) Varsayılan ayarlar ile “NEXT” seçeneğini seçerek devam ediyoruz.
###      We will continue by selecting the "NEXT" option with the default settings.


![image](https://user-images.githubusercontent.com/93924485/230357362-99abba30-6933-4cf4-94b6-1b2cb86f7296.png)


### 15-) Review Options kısmında isteğe bağlı tüm ayarlarımızı PowerShell scripti olarak görüp farklı ortamlara export edebiliriz.“NEXT” ile devam ediyoruz.
###      In the Review Options section, we can see all our optional settings as a PowerShell script and export them to different environments. We will continue by clicking "NEXT".


![image](https://user-images.githubusercontent.com/93924485/230357748-bc549e7a-5f92-46d0-9910-9c012ff9133a.png)


### 16-) Prerequisites Check kısmında domain kurulabilmesi için bir kontrol işlemi yapılmaktadır. Resimde görüldüğü üzere işlem başarılı olmuştur.”Install” ile kurulumu başlatıyoruz. Yükleme işlemi başladı. Belli bir süre sonra yükleme tamamlanacak ve sistem kendini otomatik olarak yeniden başlatacak. Kurulum sunucu özelliklerine göre 15 dakika gibi bir zaman alabilir.
###      In the Prerequisites Check section, a verification process is performed to ensure that the domain can be installed. As seen in the image, the process has been successful. We will start the installation by clicking "Install". The installation process has started. After a while, the installation will be completed, and the system will automatically restart itself. Depending on the server specifications, the installation may take around 15 minutes.


![image](https://user-images.githubusercontent.com/93924485/230358398-054cfe8e-3f9d-457a-9d04-c68f4e7caf09.png)
  

### 17-) Kurulum tamamlandıktan sonra "Domain and Computers" kısmını kontrol edelim.
###      After the installation is completed, let's check the "Domain and Computers" section.


![image](https://user-images.githubusercontent.com/93924485/230360431-aaf6ea5a-59e9-4a9f-b8bd-5cce16634854.png)


### 18-) "Node 1" isimli sunucuda kurduğumuz domain'e "Node 2" & "Node 3" sunucularını dahil edebilmek için "Node 1" sunucusunun ip adresinin "Node 2" & "Node 3" sunucularının DNS alanına yazmamız gerekmektedir.
###      We need to add the IP address of "Node 1" server to the DNS area of "Node 2" & "Node 3" servers in order to be able to join them to the domain installed on Node 1.


![image](https://user-images.githubusercontent.com/93924485/230369992-3c7f443f-96b8-4b02-8052-5dea88a5990a.png)


### 19-) Aşağıdaki adımları izleyerek "Node 2" & "Node 3" sunucularını " Raynaud.local " adlı domaine alıyoruz.
###      We are adding "Node 2" and "Node 3" servers to the domain named "Raynaud.local" by following the steps below.


![image](https://user-images.githubusercontent.com/93924485/230372682-e0891cca-ce53-48e8-bac8-24089b4d24a2.png)


![image](https://user-images.githubusercontent.com/93924485/230372748-f53b5860-8fa9-4d95-bfc5-b66417d97fe3.png)


![image](https://user-images.githubusercontent.com/93924485/230372797-fba8668f-832a-49ed-8b67-8ee29bb08a1a.png)


![image](https://user-images.githubusercontent.com/93924485/230372899-02bfae53-c43d-4976-b699-32b15ff6d1fa.png)


![image](https://user-images.githubusercontent.com/93924485/230373268-4560f67c-2894-43ab-bdeb-b56667a645d8.png)


![image](https://user-images.githubusercontent.com/93924485/230373515-fb2b2707-9038-4360-9067-957ed92ff5f1.png)


![image](https://user-images.githubusercontent.com/93924485/230373949-daaa562d-e257-4994-a0b5-6c2bc1695338.png)


• Sorunsuz bir şekilde "Node 2" & "Node 3" sunucumuzu domaine'e aldık kontrol etmek için "Node 1" de " Active Directory Users and Computers " alanından " Computers " sekmesine bakıyoruz.

• To check that we have successfully added "Node 2" and "Node 3" servers to the domain, we are looking at the "Computers" tab in the "Active Directory Users and Computers" section on Node 1.


![image](https://user-images.githubusercontent.com/93924485/230374368-2c4216c6-ba27-423c-81a0-4e9cf4e595ca.png)


### 20-) Konsolumuz açıldı. Bu sunucumuz üzerinde de buraya kadar olan işlemlerimiz tamamlandı. Şimdi cluster kurulumuna geçmeden bir test işlemi yapabiliriz. Bu adım için "Validate Configuration" linkine tıklayabiliriz.
###      Our console has been opened. We have completed all the necessary steps up to this point on this server. Now, before proceeding with the cluster installation, we can perform a test operation. For this step, we can click on the "Validate Configuration" link.


![image](https://user-images.githubusercontent.com/93924485/230376406-86fe4b91-a371-4876-b3c8-521a2240fbff.png)


![image](https://user-images.githubusercontent.com/93924485/230376479-81e61365-817e-400e-bafb-bcd35ae9ea24.png)


### 21-) Sihirbaz ekranını "Next" ile geçelim.
###      Let's proceed to the next screen of the wizard by clicking on "Next".


![image](https://user-images.githubusercontent.com/93924485/230376703-91c7bd3a-ebbd-4932-822b-528b942754c6.png)


### 22-) Test işlemini yapacak sunucuları belirlemek için Browse… butonuna tıklayalım.
###      Click on the Browse... button to select the servers that will perform the test operation.


![image](https://user-images.githubusercontent.com/93924485/230377036-f31208fd-9c83-4724-b9e0-45fedaf38947.png)


### 23-) "Node 2" & "Node 3" sunucularını bulduktan sonra "OK" butonuna tıklayalım.
###      After finding "Node 2" & "Node 3" servers, click on the "OK" button.


![image](https://user-images.githubusercontent.com/93924485/230377391-68c4b84a-2960-414a-82d9-a2bf84764cd0.png)


![image](https://user-images.githubusercontent.com/93924485/230377480-1a71312d-74af-46c0-9b28-92c33474c967.png)


![image](https://user-images.githubusercontent.com/93924485/230377827-82e9acbd-6669-48da-a246-5b6e414f876c.png)


### 24-) "Run all tests (recommended)" seçeneğini seçip tüm testlerin gerçekleşmesini sağlaman için "Next" ile sonraki adıma ilerleyelim.
###      Select the "Run all tests (recommended)" option and click "Next" to proceed to the next step to ensure that all tests are performed.


![image](https://user-images.githubusercontent.com/93924485/230378125-22a5beb9-5d0d-4601-841b-c1311f981b86.png)
 

![image](https://user-images.githubusercontent.com/93924485/230378218-d0a2c411-0cac-4157-ace9-a232d2e7cda9.png)


### 25-) Test işlemlerimiz başladı sistemdeki sorunsuzluk ve donanım özelliklerine göre kısa bir zaman dilimi bu işlemler sürecektir. 
###      Our testing process has started, and it will take a short period of time, depending on the system's stability and hardware specifications.


![image](https://user-images.githubusercontent.com/93924485/230378841-fef585ef-e6c8-48a6-814f-f0c758cc1759.png)


### 26-) Birkaç uyarı ile test işlemimiz tamamlandı. "View Report..." ile rapora göz atabilir ve sonrasında Finish ile test işlemimizi tamamlayabiliriz.
###      Our testing process has been completed with a few warnings. You can check the report by clicking on "View Report..." and then complete the testing process by clicking on "Finish".


![image](https://user-images.githubusercontent.com/93924485/230380275-8631a50d-ec1e-4eb2-a28b-43ad95245146.png)


• Testlerimizin sorunsuz olduğunu görüyoruz.

• I'm glad to hear that the tests have been successful without any issues.


# SQL Server 2019 Evaluation Edition Installation & Configuration 


### 1-) "Custom" seçeneği ile devam ediyoruz.
###     Let's proceed with the "Custom" option.


![image](https://user-images.githubusercontent.com/93924485/230628363-55e519c3-6984-49d5-870d-2db640ae7444.png)


![image](https://user-images.githubusercontent.com/93924485/230629096-dfd33d87-2e44-438b-a493-d90de7a8d1ac.png)


![image](https://user-images.githubusercontent.com/93924485/230629238-68d74658-0802-4d13-ae0a-7f83798d2a4b.png)


### 2-) "Node 1" isimli sunucumuz üzerinde SQL Server 2019 kurulumumuzu başlatalım. Biz SQL Always On mimarisi yapılandıracak olduğumuz için "New SQL Server stand-alone installation or add features to an existing installation" seçeneğine tıklayalım.
###     Let's begin the installation of SQL Server 2019 on our server named "Node 1". As we are going to configure SQL Always On architecture, we need to select the "New SQL Server stand-alone installation or add features to an existing installation" option.


![image](https://user-images.githubusercontent.com/93924485/230633310-5676e21b-e952-4d39-9db7-b53333ef1dff.png)


### 3-) "Evaluation" versiyonu ile kuruluma devam ediyoruz.
###     We will continue with the installation using the "Evaluation" version.


![image](https://user-images.githubusercontent.com/93924485/230633797-2e726251-28fc-4908-868a-a1491b503993.png)


### 4-) Sözleşmeyi kabul edip "Next" ile sonraki adıma ilerleyelim.
###     Let's accept the agreement and proceed to the next step by clicking on "Next".


![image](https://user-images.githubusercontent.com/93924485/230634101-88825807-d4c8-4083-a0ce-188e9393bef2.png)


### 5-) Use Microsoft Update to check for updates (recommended) ile güncellemeleri denetlemeniz yararlı olacaktır.
###     It would be helpful to check for updates by selecting "Use Microsoft Update to check for updates (recommended)" option.


![image](https://user-images.githubusercontent.com/93924485/230634423-44607404-5393-45de-8d1d-f2b92bfc4581.png)


### 6-) Kurulum için gerekli bileşenleri seçiyorum. Bir kurulum yaparken tüm bileşenleri yüklemek son derece yanlış bir adım. Bu nedenle bize gerekli olan SQL bileşenlerini yükleyeceğiz. Bu nedenle "Database Engine Services", "SQL Server Replication", "Full-Text and Semantic Extractions for Search" ve "Data Quality Services" bileşenlerini seçiyorum. Kurulum yapılacak olan path bilgilerine dokunmadan Next ile sonraki adıma ilerliyorum.
###     It is a good practice to only select the necessary SQL components during the installation, rather than installing all components. In this case, we will install the required SQL components, which are "Database Engine Services", "SQL Server Replication", "Full-Text and Semantic Extractions for Search", and "Data Quality Services". Let's proceed to the next step by clicking on "Next" without making any changes to the installation path information.


![image](https://user-images.githubusercontent.com/93924485/230635174-bab9f98f-a32e-4ab0-b2d5-8ae59afaf877.png)


### 7-) Bu ekranımızda kurulacak olan SQL Server için bir instance ismi belirleyebilir veya varsayılan instance ismi ile kurulum adımını geçebiliriz. Ben burada sunucu adı olarak “NODE1” instance ismini verdim. “Next” ile sonraki adıma geçiyoruz.
###     On this screen, we can either specify an instance name for the SQL Server installation or proceed with the default instance name. Here, I have provided the instance name as "NODE1", which is the same as the server name. Let's proceed to the next step by clicking on "Next".


![image](https://user-images.githubusercontent.com/93924485/230636011-48168b0b-96aa-48f0-99d7-c92f76c5ee08.png)


### 8-) "Next" ile sonraki adıma geçiyorum.
###     let's proceed to the next step by clicking on "Next".


![image](https://user-images.githubusercontent.com/93924485/230639376-0c35ba09-2936-4c78-b8dc-23eda290631f.png)


### 9-) Collation tabında özel bir dil seçiminiz olmayacak ise default olarak bırakabilirsiniz. Genelde "SQL Latin CP1_CI_AS" kullanılır.
###     If you do not have a specific language preference, you can leave the collation tab as the default setting. Generally, "SQL Latin CP1_CI_AS" is used as the collation.


![image](https://user-images.githubusercontent.com/93924485/230640282-e41f4310-403b-481f-8b1b-3393a50b009c.png)


### 10-) Database Engine Configuration kısmında kimlik doğrulama metodunu seçmemiz ve bunun için kullanıcı belirlememiz istenmektedir. Sql Server Windows kimlik doğrulaması ve Sql Server kimlik doğrulaması ile kurulabilmektedir. Biz ikisinin aynı anda aktif olma durumunu isteyebiliriz. Bu nedenle “Mixed Mode” çimini işaretliyoruz. "Add Current User" butonuna tıklayarak mevcut kullanıcımızı Windows Authentication için ekleme işlemini yapalım.
###      In the Database Engine Configuration section, we need to select the authentication method and specify the user for it. SQL Server can be installed using either Windows Authentication or SQL Server Authentication, or both can be enabled simultaneously. For this purpose, we need to select the "Mixed Mode" option. Let's check the "Mixed Mode" checkbox and click on the "Add Current User" button to add the current user for Windows Authentication. 


![image](https://user-images.githubusercontent.com/93924485/230641121-84e78e6b-e3c9-40ae-bca9-fd0e4c916d11.png)


### 11-) "Install" butonuna tıklayarak kurulumu başlatalım.
###      Let's start the installation process by clicking on the "Install" button.


![image](https://user-images.githubusercontent.com/93924485/230641587-5968ede0-eef5-4c9a-a769-f06c991b199e.png)


### 12-) Kurulum işlemi sorunsuzca tamamlandı. "Close" ile bu ekranımızı kapatabiliriz.
###      Great, the installation process has been completed successfully. We can close this window by clicking on the "Close" button.


![image](https://user-images.githubusercontent.com/93924485/230642487-7e8bd928-b155-4ba6-854e-8f18b45329f6.png)


### 13-) Kurulum sonrasında servisimiz sorunsuz start olmuş ve çalışır durumda.
###      After the installation, our service has started successfully and is running properly.


![image](https://user-images.githubusercontent.com/93924485/230643071-e5594ae5-f545-46c1-acb0-f352d2fa64db.png)


### 14-) SQL Server yönetimi için artık ayrıca kurulması gereken ve SQL Server kurulumundan bağımsız olarak kurulan SQL Management Studio kurulumunu yapalım.
###      Let's proceed to install SQL Management Studio, which is a separate installation from SQL Server and is required for SQL Server management.


![image](https://user-images.githubusercontent.com/93924485/230643881-b5cbac5a-8cfb-4bc8-9401-0b913dc43942.png)


![image](https://user-images.githubusercontent.com/93924485/230644000-3e7aefff-989c-4dc3-9927-1166336fd838.png)


![image](https://user-images.githubusercontent.com/93924485/230646542-72012eba-6795-454f-a964-adc46fc0a2f0.png)


### 15-) Windows authentication ile veritabanına login oluyoruz, login olduktan sonra veritabanı güvenliği için "Security" --> "Logins" alanından yeni bir kullanıcı tanımlamamız gerekmektedir, bu bize istediğimiz kullanıcıyı farklı yetkiler ile veritabanı üzerinde yapacağı işlemleri yönetmemize olanak sağlar.
###      We log in to the database with Windows authentication, and after logging in, for database security, we need to define a new user from the "Security" -> "Logins" area. This allows us to manage the actions that the desired user will perform on the database with different permissions.


![image](https://user-images.githubusercontent.com/93924485/230647404-7cdebba8-2c6c-4d64-bd89-eee9737a248a.png)


![image](https://user-images.githubusercontent.com/93924485/230647793-6034d069-0cb1-4ef8-b671-802ad46a6dd8.png)


• Bu zamana kadar yaptıklarımızı özetleyecek olursak, SQL Server Always On nedir bu konuya değindik, SQL Always ON mimarisini kurabilmek gerekli olan gereksinimlere değindik, SQL Server Always ON için sunucularımız üzerinde Failover Clustering özelliğini devreye alarak SQL Server 2019 kurulumlarımızı yaptık ve SQL Server yapısını yönetebilmek için gerekli olan SQL Management Studio kurulumunu yaptık. Şimdi bu kadar ön hazırlıktan sonra sıra SQL Server Always kurulumu öncesinde SQL Server cluster yapısını hayata geçirmeye.


• If we summarize what we have done so far, we have discussed what SQL Server Always On is, the requirements necessary to set up the SQL Always On architecture, we have installed SQL Server 2019 on our servers by enabling the Failover Clustering feature for SQL Server Always On, and we have installed SQL Management Studio necessary for managing the SQL Server structure. Now, after all these preparations, it is time to implement the SQL Server cluster structure before the installation of SQL Server Always On.


# Şimdi Yeni Bir Cluster Oluşturup "Node 1", "Node 2" ve "Node 3" Sunucularında Kurulu Olan SQL Server'ları Cluster'a Ekleyeceğiz.
# Now, We Will Create A New Cluster And Add The SQL Servers Installed On Node 1, Node 2, And Node 3 Servers To The Cluster.


### 1-) Node 1 sunucusu üzerinde "Failover Cluster Manager" konsolunu açalım ve konsol üzerinde "Create Cluster…" sekmesine tıklayalım.
###     Let's open the "Failover Cluster Manager" console on Node 1 server and click on the "Create Cluster..." tab on the console.


![image](https://user-images.githubusercontent.com/93924485/230717889-1e4f78f7-9d35-41a5-a6b0-9c26c3280f5a.png)


### 2-) Next ile devam edelim.
###     Let's click on "Next" to continue.


![image](https://user-images.githubusercontent.com/93924485/230718089-6f30120d-626d-4f13-9cc3-579ed6853926.png)


### 3-) Cluster’ı "Node 1" sunucusu üzerinde oluşturacağımız için ve bu cluster'a dahil olacak sunucuları belirlemek için aşağıdaki adımları sırası ile uygulayalım.
###     Since we will create the cluster on the "Node 1" server and determine the servers to be included in this cluster, let's follow the steps below in order.


• Cluster'ı oluşturmadan önce aşağıdaki komutu "Windows PowerShell" üzerinde çalıştırmalıyız.

• Before creating the cluster, we need to run the following command on "Windows PowerShell".


> Clear-ClusterNode -Name "Server name or ip "


![image](https://user-images.githubusercontent.com/93924485/230718198-d328229e-b790-4725-937f-5548fed5c3d3.png)


![image](https://user-images.githubusercontent.com/93924485/230718283-3582607d-ef89-49a5-b988-f62972d978cf.png)


![image](https://user-images.githubusercontent.com/93924485/230781774-59bef34e-b053-4d72-80fc-14bfca9d6553.png)

  
![image](https://user-images.githubusercontent.com/93924485/230781809-6eda22a0-e03b-44dd-b02e-dd157814ecfa.png)


![image](https://user-images.githubusercontent.com/93924485/230782047-c596c4c0-c066-42bc-b7d7-e3b45c21bfd8.png)



### 4-) Cluster ismini verip "Next" ile devam ediyoruz.
###     Let's give a name to the cluster and click on "Next" to continue.


![image](https://user-images.githubusercontent.com/93924485/230718487-d84aaf3e-4a94-404a-923b-adff84bba6c7.png)


### 5-) "Next" ile devam ediyoruz.
###     Let's click on "Next" to continue. 


![image](https://user-images.githubusercontent.com/93924485/230718560-0cb38b49-c673-4143-aed1-f364955db10e.png)


![image](https://user-images.githubusercontent.com/93924485/230718595-6660a5d4-2233-4b20-9b36-5f0b96d1bd0e.png)


### • Cluster'ı sorunsuz oluşturduk. Şimdi "Node2" & "Node3" sunucularını bu cluster'a dahil edelim, bunun için "Configure" alanından "Add Node" sekmesine tıklayalım.
### • We have successfully created the cluster. Now let's add "Node2" and "Node3" servers to this cluster by clicking on the "Add Node" tab in the "Configure" section. 


![image](https://user-images.githubusercontent.com/93924485/230783019-99cd42c0-9d71-4e1e-b6d9-e526a329a997.png)


• "Add Node" sekmesine tıklayın.  

• Click on "Add Node".


![image](https://user-images.githubusercontent.com/93924485/230783035-fa0d92d3-902b-409e-9a0c-8c82e2635f8b.png)


• "Next" e tıklayın.

• Click on "Next".


![image](https://user-images.githubusercontent.com/93924485/230783056-97c3550f-7846-4d8c-a0b7-30eda32ecda4.png)


• "Browse" e tıklayın.

• Click on "Browse"


![image](https://user-images.githubusercontent.com/93924485/230783081-e7533fc9-b1fd-43b0-b09d-a38639c85ea1.png)


• "Check Names" ve ardından "Advanced" a tıklayın.

• Click on "Check Names" and then click on "Advanced".


![image](https://user-images.githubusercontent.com/93924485/230783279-7bcbf8ef-a446-43c7-8ea8-ee6d2482b423.png)


• Ve "Find Now" a tıklayarak "Node2" & "Node3" sunucularını ekliyoruz.

• We add "Node2" and "Node3" servers by clicking on "Find Now" after that.


![image](https://user-images.githubusercontent.com/93924485/230783383-9f6fa7e7-d317-49e5-bb91-72d4f91b0bb7.png) 


![image](https://user-images.githubusercontent.com/93924485/230783572-efd385ac-25ae-457c-a09a-a145567761b1.png)


• "Next" e tıklayın.

• Click on "Next"


![image](https://user-images.githubusercontent.com/93924485/230783521-59ac37cd-98e5-4707-880c-7c536ae4e4ac.png)


• "Next" e tıklayın.

• Click on "Next"


![image](https://user-images.githubusercontent.com/93924485/230783618-66b067c2-35fb-4f09-970c-ee11f6b8b065.png)


![image](https://user-images.githubusercontent.com/93924485/230783645-cdaee09a-e395-4f27-8f66-68fc172f7483.png)


![image](https://user-images.githubusercontent.com/93924485/230783675-e15301a7-dd7b-40ec-8c6c-ff126ff18005.png)


# Nihayet sıra geldi SQL Always On mimarisini devreye almaya !
# Finally, it's time to implement the SQL Always On architecture !


### • "Node1" sunucusunda "Failover Cluster Manager" üzerinde "Raynaud" adında yeni bir cluster oluşturarak ve "Node2" & "Node3" isimli sunucularımızı cluster ortamına dahil ettik. Always On mimarisi yapılandırma adımları öncesinde birkaç ön hazırlık yapmamız gerekiyor.
### • Before configuring the Always On architecture, we need to make a few preparations. We have created a new cluster named "Raynaud" on the "Node1" server using the "Failover Cluster Manager" and added our servers named "Node2" and "Node3" to the cluster environment.


### 1-) "SQL Server Configuration Manager" konsolunu açalım. "SQL Server Network Configuration altında" yer alan "Protocols for NODE1" isimli instance’ımıza ait ekranı açalım. Disable durumda olan "Named Pipes ekranını açalım". 
###     Let's open the "SQL Server Configuration Manager" console and access the screen for the "Protocols for NODE1" instance under "SQL Server Network Configuration". Let's open the "Named Pipes screen" while in disabled state.


![image](https://user-images.githubusercontent.com/93924485/230890320-d53eb2f3-8e89-411b-9b81-19c451442569.png)


### 2-) "Named Pipes Properties" ekranımızdaki "Enabled" özelliğini "Yes" konumuna getirelim. "OK" ile bu ekrandan çıkalım.
###     Let's set the "Enabled" property to "Yes" on our "Named Pipes Properties" screen. Then, let's exit this screen by clicking on "OK".


![image](https://user-images.githubusercontent.com/93924485/230890921-cba74b29-61c4-4e9f-8447-6eb69572de1f.png)


### 3-) Sonrasında "Node1" instance özelliklerini açarak "Enable Qlways On Availability Groups" özelliğini aktif duruma getirerek "OK" butonu ile bu ekranımızdan çıkalım.
###     After that, let's open the properties of the "Node1" instance, enable the "Enable Always On Availability Groups" feature, and exit this screen by clicking on the "OK" button.


• Bu işlemin aynısını "Node2" & "Node3" sunucularında da yapmamız gerekiyor.

• We need to perform the same operation on 'Node2' & 'Node3' servers as well.


![image](https://user-images.githubusercontent.com/93924485/230933869-5da58a2b-15dc-4807-ad58-97395a3dea9d.png)


![image](https://user-images.githubusercontent.com/93924485/230934127-50fbf8da-211a-4aea-b5ca-6b7318521c29.png)


• Always On konfigürasyon için gerekli SQL Server versionu aşağıdaki gibi olmalıdır.

• The required SQL Server version for configuring Always On should be as follows.


![image](https://user-images.githubusercontent.com/93924485/230948013-c7f197e6-8917-4224-998d-325de4d74664.png)


![image](https://user-images.githubusercontent.com/93924485/230949881-782457f6-0725-46b1-a8ef-b2cc6507b683.png)


• "Node1" Sunucumuzda "SQL Server 2019" kurulumu yaparken "Active Directory Domain Services" & "Active Directory Web Services" servislerini "Disable" a çekmemiz gerekiyor yoksa "Always On" özelliğini devreye alamayız !

• When installing SQL Server 2019 on our "Node1" server, we need to disable the "Active Directory Domain Services" and "Active Directory Web Services" services, otherwise we won't be able to activate the "Always On" feature.


![image](https://user-images.githubusercontent.com/93924485/231206866-9709f727-29bb-4585-b273-fb56e060c6d6.png)


### 4-) "Node 2" sunucumuz üzerindeki SQL veritabanına "SQL Management Studio" ile bağlanalım ve "Always On High Availability" sekmesine tıklayalım, altında "Availability Groups" sekmesi sorunsuzca açılıyor. Bu sekme üzerinde sağ tıklayarak "New Availability Group Wizard…"  sekmesine tıklayarak artık "Always On" konfigürasyonunu başlatabiliriz. 
###     Let's connect to the SQL database on our "Node 2" server using "SQL Management Studio" and click on the "Always On High Availability" tab. The "Availability Groups" tab opens smoothly. Right-click on this tab and click on the "New Availability Group Wizard..." tab to start configuring "Always On".


![image](https://user-images.githubusercontent.com/93924485/231478615-fa7c5a13-8c63-4f52-a841-4c97ef7c7355.png)


• "Next" e tıklayın.

• Click on "Next"


![image](https://user-images.githubusercontent.com/93924485/231479128-1a47ab54-cf2e-4b0c-a9db-9eb72a35a15c.png)


### 5-) Biz  "Windows Failover Cluster" kullanacağımız için seçimimizi bu şekilde ayarlayarak "Windows Server Failover Cluster" seçimini yapıyoruz.
###     We are choosing "Windows Server Failover Cluster" option by setting our selection in this way, as we will be using "Windows Failover Cluster".


![image](https://user-images.githubusercontent.com/93924485/231480204-6c987d38-a4a7-4ae3-87bd-68d5ab04721d.png)


### 6-) İşlemlere başlamadan önce işlem yapılacak olan database özelliğinin "Full Recovery Mode" yapısında olması isteniyor. Bu gereksinimi yerine getirmeden ilerleyemeyiz. Bu demek oluyor ki Always On mimarisi içerisine girerek olan database "Full Recovery Mode" yapısında olmak zorunda. Bunun için aşağıdaki adımları izleyin.
###     Before starting the process, it is required that the database to be processed is in "Full Recovery Mode". We cannot proceed without meeting this requirement. This means that the database within the Always On architecture must be in "Full Recovery Mode". Follow the steps below to achieve this.


• ![image](https://user-images.githubusercontent.com/93924485/231482439-85b7ee38-a5bd-4ca5-b082-acffac2bf915.png)

• ![image](https://user-images.githubusercontent.com/93924485/231482793-7377fc11-c6f6-43af-8820-332283d64973.png)


### 7-) Yedekleme işlemini gerçekleştirmek için ana konsolda veritabanına sağ tıklayıp "Tasks" seçeneğine tıklayın ve ardından 'Backup' menüsüne tıklayın.
###     To perform the backup process, right-click on the database in the main console, click on "Tasks", and then click on "Backup" menu.


![image](https://user-images.githubusercontent.com/93924485/231484658-f3080893-e528-4a1e-a469-1ea03a3d9b1f.png)


![image](https://user-images.githubusercontent.com/93924485/231485330-b460fbb0-eee0-4ecc-954d-f22c54eb49fc.png)


![image](https://user-images.githubusercontent.com/93924485/231485495-853016d3-6f65-42ed-ab12-9a18fd31960e.png)


![image](https://user-images.githubusercontent.com/93924485/231485845-69efdf36-146f-4850-8357-aaba759f2026.png)


















