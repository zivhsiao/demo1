---
layout: post
title: "MAMP Pro 與 Vagrant 以及 docker 的比較"
author: patrick
categories: [開發工具]
image: "https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp_vagrant_docker/vagrant-docker-mamp.png"  
tag: featured
---

因爲筆者是使用 Macbook Pro，所以早期是使用 MAMP Pro 4 當作 PHP 以及 mySQL 的開發機，最近又因爲 PHP 的關係才升級到 5.x ，這時才有支援 7 以上，目前是支援 7.3.1

基本是用 PHP 7.2.14，因爲 PHP 改成 7.3.1 之後，Laravel 似乎會容易造成 JIT 記憶體不足的問題，這個就不管它了，能夠跑起來最重要就好了

所以基本的搭配是 PHP 7.2.14、MySQL 5.7.25，它要建立一個網站就單純的點一點，測試的網址給它就完成了，幾乎都沒有什麼好等待，不過因爲是 Laravel 加 Voyager 所以還是要等他的下載

下面的圖案就是 MAMP Pro 5.x 的管理界面

![mamp_pro](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp_vagrant_docker/mamp_1.png) 

![mamp_pro](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp_vagrant_docker/mamp_2.png)

### 先改用 Vagrant 容器

![vagrant](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp_vagrant_docker/vagrant_virtualbox.png)

這是從 wiki 截取下來的一段話

> Vagrant 是一款用於構建及配置虛擬開發環境的軟體，基於Ruby,主要以命令行的方式運行。
>
> 主要使用 Oracle 的開源 VirtualBox 虛擬化系統，與 Chef，Salt，Puppet 等環境配置管理軟體搭配使用， 可以實行快速虛擬開發環境的構建。

從這裏不難看出它是用來做什麼的，直接告訴你它是利用虛擬機來打造一個屬於自己的開發機，它與虛擬機的差異在於下指令就可以完成，不用靠使用者界面去完成它

一開始對於它是有興趣，不外乎是下下指令就可以達成你想要的容器了，甚至你的容器是可以上傳到它的網站，供其它人去使用

使用它還有一個原因，可以做到負載平衡，不過因爲要負載平衡的案子幾乎沒有，而且它主要是透過虛擬機，所以都要時間等他 up，所以也沒有就會用到它，所以就沒有機會去用到它了




## 後來又改爲 docker 容器

![docker](https://raw.githubusercontent.com/zivhsiao/repo-picture-1/master/images/mamp_vagrant_docker/docker.png)

docker wiki 有一段話

> Docker 是一個開放原始碼軟體專案，讓應用程式部署在軟體貨櫃下的工作可以自動化進行，藉此在 Linux 作業系統上，提供一個額外的軟體抽象層，以及作業系統層虛擬化的自動管理機制。
>
> Docker 利用Linux核心中的資源分離機制，例如cgroups，以及Linux 核心命名空間（namespaces），來建立獨立的容器（containers）。這可以在單一 Linux 實體下運作，避免啟動一個虛擬機器造成的額外負擔[2]。Linux 核心對命名空間的支援完全隔離了工作環境中應用程式的視野，包括行程樹、網路、用戶 ID 與掛載檔案系統，而核心的 cgroup 提供資源隔離，包括CPU、記憶體、block I/O與網路。從 0.9 版本起，Dockers 在使用抽象虛擬是經由 libvirt 的 LXC 與 systemd - nspawn 提供介面的基礎上，開始包括libcontainer 函式庫做為以自己的方式開始直接使用由 Linux 核心提供的虛擬化的設施，

說的白話一點，就是它只有底層在跑，之後有個 docker-composer 可以讓 docker 跑得更加容易，譬如加入一個 web 就寫一段程式就可以跑起來，加入 db 就要給它一個 db 的宣告就可以了，這些統統可以在  docker-composer 裏面可以實現，不用管他怎麼跑的，只要透過 docker 以及 docker-composer 就可以了

不過有個問題來了，就是它的效能在 Macbook Pro 底下，實在是非常慢，當我跑起來的時候，大概要等 10~20 秒之後才會出現我的測試網頁，然後每一次切換頁面要等待的時間，每一次 down 然後 up 的狀況都是這樣

這就讓我覺得奇怪，google 了一下，得到的回應是作業系統的關係，變成要靠虛擬機？問題是就不要用虛擬機才用 docker，結果是因爲 OS 的不同而要用虛擬機，這不是反過來用 vagrant 就好了？

### 所以放棄容器的概念，而又轉回 MAMP Pro

所以如果是 Mac 在開發一個網站，直接用 MAMP Pro 可能比較快，而且又可以上傳到 github or gitlab

這裏或許不是每個 Mac 都會遇到，至少我遇到過，所以我不想用虛擬機，而且 docker 讓我用的很難過，所以直接放棄

MAMP Pro 是開發網站的好幫手啊！

