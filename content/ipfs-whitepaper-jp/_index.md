---
title: 【参考】whitepaper 日本語訳
weight: 7
pre: "<b>7. </b>"
---
本章は参考情報として[Juan Benet](juan@benet.ai)によって書かれたIPFSの[whitepaper](https://ipfs.io/ipfs/QmR7GSQM93Cx5eAg6a6yRzNde1FQv7uL6X1o4k7zrJa3LX/ipfs.draft3.pdf)「IPFS-Content Addressed, Versioned, P2P File System (DRAFT 3)」の日本語訳を記します。

※ 翻訳は直訳を避け、原文の内容を損ねない範囲で（大幅に）意訳しています。そのため必要な場合は[原文](https://ipfs.io/ipfs/QmR7GSQM93Cx5eAg6a6yRzNde1FQv7uL6X1o4k7zrJa3LX/ipfs.draft3.pdf)を参照ください。

## 概要
Inter Planetary File System(IPFS)はピアツーピア型の分散型ファイルシステムであり、全てのデバイスを一つのファイルシステムに結合することを目的としたものです。いくつもの点でIPFSはWebと同様のもの言えますが、一方で、一つのGitリポジトリ上でオブジェクト交換を行うBitTorrentのスウォームと考えることもできます。またはコンテンツアドレス型のハイパーリンク機能をもつストレージとも考えられます。IPFSはMerkle-DAGのデータ構造を持ちます。IPFS上にバージョン管理可能なファイルシステムやブロックチェーン、または永続的なWebを構築することが可能になります。IPFSは分散ハッシュテーブル技術、インセンティブが与えられたブロック交換技術、自己証明型名前空間といった要素技術を組み合わせて実現されており、単一障害点がなくピア同士がお互いの信頼を必要とせずに実現できるシステムです。

## 1. 序論
これまで多くのグローバルな分散ファイルシステムを構築する試みがなされてきました。いくつかは顕著な成果を見せましたが、その他は完全に失敗に終わりました。例えば学術的な取り組みとしては、AFS[6]が成功事例として挙げられ現在も活用されている一方で、その他[7,?]の試みは失敗に終わっています。学術的な試み以外でのピアツーピア型の分散ファイルシステムは大容量コンテンツ（音楽や動画など）の共有用途に発展してきました。特にNapsterやKaZaA、BitTorrent[2]といったアプリケーションは1億人以上のユーザーによって支えられる巨大な分散システムでした。今日でもBitTorrentは1,000万ものノードが動作している巨大なファイルシステムとして動作し続けています[16]。これらのアプリケーションは、学術的な取り組みの中でのファイルシステムよりも多くのユーザーを惹きつけてきました。しかしこれらは別目的で利用される事例[^1]はあるものの、あくまでアプリケーションであり、その上でシステムやアプリケーションが動作するインフラ基盤としてデザインされているものではありません。その点で、一般的なファイルシステムとして利用可能な、グローバル規模で低レイテンシー分散ファイルシステムというものはこれまで現れてきていないといえます。

この理由は既に十分良いシステムが存在していたからと考えられます。「HTTP」です。HTTPはこれまで最も成功した分散ファイルシステムプロトコルです。ブラウザと結びつくことでHTTPは技術的にも社会的にも多くのインパクトを与え、インターネット上でのファイル転送のデファクトスタンダードとなっています。しかしHTTPはそれが世に出て以降の15年の間に生み出されてきた新たな技術を取り込むことには失敗しています。多くの後方互換性の確保やステークホルダーの複雑なしがらみから、Webのインフラ基盤を進化させることは事実上不可能に見える一方で、実際にはHTTPの出現以降も様々な新しいプロトコルが生み出され広範囲で利用されている事実もあります。ユーザーエクスペリエンスを損なうことなく新たな機能を導入するようなHTTP-Webのグレードアップを行なっていく必要があります。

HTTPプロトコルは小容量のデータのやりとりに関して比較的安価で行うことを実現する一方で我々はデータ転送に関して新たな時代に突入しつつあります。それは(a)ペタバイト級データのホストと配信 (b)組織横断の大量データ処理 (c)大容量高精細なオンデマンドのコンテンツストリーミング(d)大規模データのバージョン管理およびリンク処理(e)重要データの消失防止、というようなものが要求される時代です。このような状況のもと、我々はHTTPを捨てて新たなデータ転送プロトコルを開発しました。次のステップはこれをWebそのものにすることが必要です。

データ転送と同等に、バージョン管理技術はデータ操作の協調作業に重要な役割を果たしてきました。ソースコード分散バージョン管理システムであるGitは分散されたデータ操作の実装モデルとして非常に重要であり、Git関連技術は従来の大容量ファイルシステムにはなかったバージョン管理機能の実現を可能にします。Camlistore[?]やDat[?]といったGitにインスパイアされたシステムも出現しています。またGitは「コンテンツアドレスMerkle-DAG」形式のデータモデルを採用しており、この方式は既に分散ファイルシステムに影響を与えています。

本論文ではバージョン管理機能を備えた新しいファイルシステムであるIPFSについて解説します。IPFSの中心指針は「全てのデータを統一されたMerkle-DAGにモデリングする」というものです。

（以降追記予定）


## 7. Reference

［1］ I. Baumgart and S. Mies. S/kademlia:
A practicable approach towards secure key-based routing. In Parallel and Distributed Systems, 2007 International Conference on, volume 2, pages 1–8. IEEE, 2007.

[2] I. BitTorrent. Bittorrent and A¸ttorrent software ˆ
surpass 150 million user milestone, Jan. 2012.

[3] B. Cohen. Incentives build robustness in bittorrent. In
Workshop on Economics of Peer-to-Peer systems,
volume 6, pages 68–72, 2003.

[4] J. Dean and S. Ghemawat. leveldb–a fast and
lightweight key/value database library by google, 2011.

[5] M. J. Freedman, E. Freudenthal, and D. Mazieres.
Democratizing content publication with coral. In
NSDI, volume 4, pages 18–18, 2004.

[6] J. H. Howard, M. L. Kazar, S. G. Menees, D. A.
Nichols, M. Satyanarayanan, R. N. Sidebotham, and
M. J. West. Scale and performance in a distributed file
system. ACM Transactions on Computer Systems
(TOCS), 6(1):51–81, 1988.

[7] J. Kubiatowicz, D. Bindel, Y. Chen, S. Czerwinski,
P. Eaton, D. Geels, R. Gummadi, S. Rhea,
H. Weatherspoon, W. Weimer, et al. Oceanstore: An
architecture for global-scale persistent storage. ACM
Sigplan Notices, 35(11):190–201, 2000.

[8] D. Levin, K. LaCurts, N. Spring, and
B. Bhattacharjee. Bittorrent is an auction: analyzing
and improving bittorrent’s incentives. In ACM
SIGCOMM Computer Communication Review,
volume 38, pages 243–254. ACM, 2008.

[9] A. J. Mashtizadeh, A. Bittau, Y. F. Huang, and
D. Mazieres. Replication, history, and grafting in the
ori file system. In Proceedings of the Twenty-Fourth
ACM Symposium on Operating Systems Principles,
pages 151–166. ACM, 2013.

[10] P. Maymounkov and D. Mazieres. Kademlia: A
peer-to-peer information system based on the xor
metric. In Peer-to-Peer Systems, pages 53–65.
Springer, 2002.

[11] D. Mazieres and F. Kaashoek. Self-certifying file
system. 2000.

[12] D. Mazieres and M. F. Kaashoek. Escaping the evils
of centralized control with self-certifying pathnames.
In Proceedings of the 8th ACM SIGOPS European
workshop on Support for composing distributed
applications, pages 118–125. ACM, 1998.

[13] J. Rosenberg and A. Keranen. Interactive connectivity
establishment (ice): A protocol for network address
translator (nat) traversal for offer/answer protocols.
2013.

[14] S. Shalunov, G. Hazel, J. Iyengar, and M. Kuehlewind.
Low extra delay background transport (ledbat).
draft-ietf-ledbat-congestion-04. txt, 2010.

[15] R. R. Stewart and Q. Xie. Stream control transmission
protocol (SCTP): a reference guide. Addison-Wesley
Longman Publishing Co., Inc., 2001.

[16] L. Wang and J. Kangasharju. Measuring large-scale
distributed systems: case of bittorrent mainline dht. In
Peer-to-Peer Computing (P2P), 2013 IEEE Thirteenth
International Conference on, pages 1–10. IEEE, 2013.
ß

[^1]: 例えば、Linuxはディスクイメージの配布のためにBitTorrentを利用したり、Blizzard,Inc.はビデオゲームの配布のために利用したりしています。