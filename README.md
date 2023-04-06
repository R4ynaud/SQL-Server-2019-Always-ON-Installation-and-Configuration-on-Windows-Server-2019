# SQL-Server-2019-Always-ON-Installation-and-Configuration-on-Windows-Server-2019

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


### 5-) Bu özellik ekleme işlemi sırasında yeniden başlatma gerekir ise bunun otomatik olarak gerçekleşmesi için Restart the destination server automatically if requred seçimini işaretleyebiliriz. Ben gerekmesi durumunda bunu manuel olarak yapacağım için kurulum adımlarını başlatıp tamamlamak için Install butonuna tıklıyorum.
###     We can select "Restart the destination server automatically if required" option if a restart is needed during the feature addition process to be done automatically. However, if you prefer to do this manually, you can start and complete the installation steps by clicking on the "Install" button.


![image](https://user-images.githubusercontent.com/93924485/230314919-0976ac8d-6bde-42a3-987a-950abb21c33a.png)


### 6-) Failover Cluster Manager konsolumuzu açabiliriz.
###     Sure, we can open the Failover Cluster Manager console.


![image](https://user-images.githubusercontent.com/93924485/230316080-db9d30ac-6fa0-4102-a9a8-ce408927dfb3.png)


### 7-) Konsolumuz açıldı. Bu sunucumuz üzerinde buraya kadar olan işlemlerimiz tamamlandı. Aynı işlemleri diğer sunucularımız üzerinde gerçekleştireceğiz.
###     Great! The console is now open. We have completed the necessary steps on this server. We can now proceed to perform the same steps on our other servers.


![image](https://user-images.githubusercontent.com/93924485/230316504-5b7cafe3-7d5b-44e8-808c-5cf0a6f99abb.png)


### 8-) Cluster kurulumuna geçmeden önce tüm sunucularda Active Directory Domain Services kurulumu yapmamız gerekiyor, bunun için aşağıdaki adımları uygulayabilirsiniz. 
###     Before proceeding with the cluster installation, we need to install Active Directory Domain Services on all servers. You can follow the steps below for this.


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


### 12-) DNS Options kısmında bir uyarı çıkıyor.Bu uyarı herhangi bir problem teşkil etmektedir.Yapımızda bir DNS Server olmadığı  ve DNS Zone üzerinde herhangi bir Delegasyon ataması yapılmadığı için vermektedir.“NEXT” ile devam ediyorum.
###      There is a warning in the DNS Options section. This warning does not pose any problems. It is displayed because there is no DNS Server in our structure and no delegation is assigned on the DNS Zone. I will proceed by clicking "NEXT".


![image](https://user-images.githubusercontent.com/93924485/230356397-a6be4510-89b1-483d-a014-5eccc2cfc2a1.png)


### 13-) Addition Options kısmında domain yapısı için otomatik olarak oluşan NETBIOS name ismini görüyoruz.(NETBIOS yerel ağ üzerindeki farklı bilgisayarların birbiriyle iletişim kurmasını sağlayan bir sistemdir.) “NEXT” ile devam ediyoruz.
###      In the Addition Options section, we see the NETBIOS name that is automatically generated for the domain structure. (NETBIOS is a system that enables different computers on the local network to communicate with each other.) We will proceed by clicking "NEXT".


![image](https://user-images.githubusercontent.com/93924485/230356958-5deec787-a72e-4b11-9a38-b3a732febb7c.png)


### 14-) Varsayılan ayarlar ile “NEXT” seçeneğini seçerek devam ediyoruz.
###      We will continue by selecting the "NEXT" option with the default settings.


![image](https://user-images.githubusercontent.com/93924485/230357362-99abba30-6933-4cf4-94b6-1b2cb86f7296.png)


### 15-) Review Options kısmında isteğe bağlı tüm ayarlarımızı powershell scripti olarak görüp farklı ortamlara export edebiliriz.“NEXT” ile devam ediyoruz.
###      In the Review Options section, we can see all our optional settings as a PowerShell script and export them to different environments. We will continue by clicking "NEXT".


![image](https://user-images.githubusercontent.com/93924485/230357748-bc549e7a-5f92-46d0-9910-9c012ff9133a.png)


### 16-) Prerequisites Check kısmında domain kurulabilmesi için bir kontrol işlemi yapılmaktadır. Resimde görüldüğü üzere işlem başarılı olmuştur.”Install” ile kurulumu başlatıyoruz.Yükleme işlemi başladı.Belli bir süre sonra yükleme tamamlanacak ve sistem kendini otomatik olarak yeniden başlatacak.Kurulum sunucu özelliklerine göre 15 dakika gibi bir zaman alabilir.
###      In the Prerequisites Check section, a verification process is performed to ensure that the domain can be installed. As seen in the image, the process has been successful. We will start the installation by clicking "Install". The installation process has started. After a while, the installation will be completed, and the system will automatically restart itself. Depending on the server specifications, the installation may take around 15 minutes.


![image](https://user-images.githubusercontent.com/93924485/230358398-054cfe8e-3f9d-457a-9d04-c68f4e7caf09.png)
  

### 17-) Kurulum tamamlandıktan sonra Domain and Computers kısmını kontrol edelim.
###      After the installation is completed, let's check the Domain and Computers section.


![image](https://user-images.githubusercontent.com/93924485/230360431-aaf6ea5a-59e9-4a9f-b8bd-5cce16634854.png)


### 18-) Node 1 isimli sunucuda kurduğumuz doamine Node 2 & Node 3 sunucularını dahil edebilmek için Node 1 sunucusunun ip adresinin Node 2 & Node 3 sunucularının DNS alanına yazmamız gerekmektedir.
###      We need to add the IP address of Node 1 server to the DNS area of Node 2 & Node 3 servers in order to be able to join them to the domain installed on Node 1.


![image](https://user-images.githubusercontent.com/93924485/230369992-3c7f443f-96b8-4b02-8052-5dea88a5990a.png)


### 19-) Aşağıdaki adımları izleyerek Node 2 & Node 3 sunucuları " Raynaud.local " adlı domaine alıyoruz.
###      We are adding Node 2 and Node 3 servers to the domain named "Raynaud.local" by following the steps below.


![image](https://user-images.githubusercontent.com/93924485/230372682-e0891cca-ce53-48e8-bac8-24089b4d24a2.png)


![image](https://user-images.githubusercontent.com/93924485/230372748-f53b5860-8fa9-4d95-bfc5-b66417d97fe3.png)


![image](https://user-images.githubusercontent.com/93924485/230372797-fba8668f-832a-49ed-8b67-8ee29bb08a1a.png)


![image](https://user-images.githubusercontent.com/93924485/230372899-02bfae53-c43d-4976-b699-32b15ff6d1fa.png)


![image](https://user-images.githubusercontent.com/93924485/230373268-4560f67c-2894-43ab-bdeb-b56667a645d8.png)


![image](https://user-images.githubusercontent.com/93924485/230373515-fb2b2707-9038-4360-9067-957ed92ff5f1.png)


![image](https://user-images.githubusercontent.com/93924485/230373800-ee5a4fb4-0034-4468-8913-8359d888cbce.png)


![image](https://user-images.githubusercontent.com/93924485/230373949-daaa562d-e257-4994-a0b5-6c2bc1695338.png)





