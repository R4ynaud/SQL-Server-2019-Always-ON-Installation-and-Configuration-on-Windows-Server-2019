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


