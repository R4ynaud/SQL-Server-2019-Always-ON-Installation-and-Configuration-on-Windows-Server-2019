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


### 2-) Açılan ekranımızda iki seçeneğimiz yer almaktadır. Bunlardan birincisi olan;

• Role-based or feature-based insallation : Rol ve Özellik bazında ekleme kurulum yapma imkânı verir. Windows Server 2019 içerisinde sahip olduğumuz sürüme göre, içerisinde bulunan ve ihtiyacımız olan rol ve özellikleri buradan ekleyip kaldırabilmekteyiz.

• Remote Desktop Services installation: Eski zamanlarda Terminal Servis olarak anılan ve şimdi RDS (Remote Desktop Services) uzak masaüstü yapılandırmasını hızlı ve standart olarak buradan yapabilmekteyiz.

• Bu nedenle biz Failover Clustering özelliğini kuracak olduğumuz için Role-based or feature-based insallation seçimini yaparak Next ile ilerliyoruz.
