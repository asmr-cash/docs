.. _block_contract_upgraded:

Block 主合约升级完毕
============================

``BNET`` 旧合约 ``0x3F1...2F5`` 已经弃用，快照于 ``2019-04-15 00:00:00 UTC
标准时间``，历史账户数据经  完成迁移。

|logo_etherscan_verified| |logo_github| |logo_verified|

- ENS 域名 **blockdao.eth**
- 合约地址 **0x82070415FEe803f94Ce5617Be1878503e58F0a6a**
- 部署于 `Tx Hash 0x9f173f8fc13a8efef7cb25b160c09958...`_
- 区块高度 `7635415`_
- 已经在 `GNU 通用公区许可证 v3.0`_ 协议下开源
- `查看合约代码在 github 仓库`_

在 Etherscan.io 查看：

- `Block 跟踪`_
- `通过 Etherscan.io 读取合约信息`_
- `通过 Etherscan.io 操作合约`_

.. _Tx Hash 0x9f173f8fc13a8efef7cb25b160c09958...: https://etherscan.io/tx/0x9f173f8fc13a8efef7cb25b160c09958be03587b9b1af910bf8a9b3a48d68dc9
.. _7635415: https://etherscan.io/tx/0x9f173f8fc13a8efef7cb25b160c09958be03587b9b1af910bf8a9b3a48d68dc9
.. _GNU 通用公区许可证 v3.0: https://github.com/blockdao/contracts/blob/master/LICENSE
.. _查看合约代码在 github 仓库: https://github.com/blockdao/contracts/blob/master/Block.sol
.. _Block 跟踪: https://etherscan.io/token/0x82070415fee803f94ce5617be1878503e58f0a6a
.. _通过 Etherscan.io 读取合约信息: https://etherscan.io/token/0x82070415fee803f94ce5617be1878503e58f0a6a#readContract
.. _通过 Etherscan.io 操作合约: https://etherscan.io/token/0x82070415fee803f94ce5617be1878503e58f0a6a#writeContract

.. |logo_github| image:: /_static/logos/github.svg
   :width: 36px
   :height: 36px

.. |logo_etherscan_verified| image:: /_static/logos/etherscan_verified.svg
   :width: 36px
   :height: 36px

.. |logo_verified| image:: /_static/logos/verified.svg
   :width: 36px
   :height: 36px


新的字母符号 ``Block``
------------------------------------

用于在各种钱包软件和以太坊区块链浏览器中显示，比如 `MetaMask`_, `MyEtherWallet`_, `imToken`_, 
`etherscan.io`_ 等。

.. _MetaMask: https://metamask.io/
.. _MyEtherWallet: https://www.myetherwallet.com/
.. _imToken: https://imkey.im/
.. _etherscan.io: https://etherscan.io/


使用价值锚定保持不变
------------------------------------------

在区块网络的生态体系中 ``1 Block`` 与 ``dao 客户端流量`` 关联。

新合约已经全面优化
--------------------------------

受益于以太坊主网的 `君士坦丁堡`_ 和 `君士坦丁堡/圣彼得堡`_ 这两次升级所带来的全新特性，**新合约的运行效率得到了极大的提升**。

.. _君士坦丁堡: https://blog.ethereum.org/2019/01/11/ethereum-constantinople-upgrade-announcement/
.. _君士坦丁堡/圣彼得堡: https://blog.ethereum.org/2019/02/22/ethereum-constantinople-st-petersburg-upgrade-announcement/


Block 的转账以太坊 **矿工费大幅节省** ，**最高节省达 30.19%** 。


--------------------------------------------------

发送 1,001 Blocks 到一个白名单中的地址，您的 ETH 以太坊钱包地址将被 **自动注册** 

白名单资格支持过户
---------------------------------------------

:ref:`whitelist_transfer_whitelist_qualification`

不需要经过任何申请和审批流程，直接调用合约功能 ``transferWhitelist(address account)`` 
即可完成，智能合约将会自动立即处理。
