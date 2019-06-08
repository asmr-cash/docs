.. _block_contract:

Block 主合约
===================

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

相关链接：

- :ref:`block_contract_upgraded`


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



读懂 Block 合约
-------------------------

如果您想深入了解 Block 合约，这将帮助到您。


元信息
__________

.. code-block:: text

   // solidity

   string private _name = "Block.Network dao Token";
   string private _symbol = "ABC";
   uint8 private _decimals = 6;                // 6 decimals
   uint256 private _cap = 35000000000000000;   // 35 billion
   uint256 private _totalSupply;

全名
   Block.Network dao Token

字母简称
   Block

小数位数
   6

封顶的总供应量
   350 亿


Block 销售白名单注册触发
_________________________________________

.. code-block:: text

   // solidity

   function transfer(address to, uint256 value) public whenNotPaused returns (bool) {
       if (_allowWhitelistRegistration && value == _whitelistRegistrationValue
           && inWhitelist(to) && !inWhitelist(msg.sender) && isNotContract(msg.sender)) {
           // Register whitelist for Block-Sale
           _regWhitelist(msg.sender, to);
           return true;
       } else {
           // Normal Transfer
           _transfer(msg.sender, to, value);
           return true;
       }
   }


- ``_allowWhitelistRegistration`` 是 ``true``，即主合约处在可注册的状态。
- ``value`` = ``_whitelistRegistrationValue`` ，即转账数量是 1,001 Blocks 。
- ``inWhitelist(to)`` ，接收地址已经在白名单中。
- ``!inWhitelist(msg.sender)`` ，发送地址不在白名单中。
- ``isNotContract(msg.sender)`` 
  ，发送地址不是合约，以避免任何来自合约转账的“巧合的意外”，包括“任何形式的批量转账”、“来自交易所的发送” 或其它任何形式的合约。

除在此特殊条件下的转账，都被视为 **普通转账** 。


Block-Sale Whitelist Registration and Referral Reward
_____________________________________________________

.. code-block:: text

   // solidity

   uint256 private _whitelistRegistrationValue = 1001000000;   // 1001 Block
   uint256[15] private _whitelistRefRewards = [                // 100% Reward
       301000000,  // 301 Block for Level.1
       200000000,  // 200 Block for Level.2
       100000000,  // 100 Block for Level.3
       100000000,  // 100 Block for Level.4
       100000000,  // 100 Block for Level.5
       50000000,   //  50 Block for Level.6
       40000000,   //  40 Block for Level.7
       30000000,   //  30 Block for Level.8
       20000000,   //  20 Block for Level.9
       10000000,   //  10 Block for Level.10
       10000000,   //  10 Block for Level.11
       10000000,   //  10 Block for Level.12
       10000000,   //  10 Block for Level.13
       10000000,   //  10 Block for Level.14
       10000000    //  10 Block for Level.15
   ];

.. code-block:: text

   // solidity

   function _regWhitelist(address account, address refAccount) internal {
       _refCount[refAccount] = _refCount[refAccount].add(1);
       _referrer[account] = refAccount;

       emit BlockSaleWhitelistRegistered(account, refAccount);

       // Whitelist Registration Referral Reward
       _transfer(msg.sender, address(this), _whitelistRegistrationValue);
       address cur = account;
       uint256 remain = _whitelistRegistrationValue;
       for(uint i = 0; i < _whitelistRefRewards.length; i++) {
           address rcv = _referrer[cur];
           if (cur != rcv) {
               if (_refCount[rcv] > i) {
                   _transfer(address(this), rcv, _whitelistRefRewards[i]);
                   remain = remain.sub(_whitelistRefRewards[i]);
               }
           } else {
               _transfer(address(this), refAccount, remain);
               break;
           }
           cur = _referrer[cur];
       }
   }

转账 1,001 Blocks 到白名单中的地址
   将触发 Block 销售白名单注册。

1,001 Blocks 的 100% 将用于发放奖励
   最多 15 级：301 + 200 + 100 + ...


.. _check_address_in_whitelist:

查看一个 ETH 钱包地址是否在白名单中
_________________________________________________

.. code-block:: text

   // solidity

   function inWhitelist(address account) public view returns (bool) {
       return _referrer[account] != address(0);
   }

查看一个 ETH 钱包地址是否在白名单中
   执行合约中的功能函数 ``inWhitelist(address account)`` ，如果给定的地址已在白名单中，则返回 ``true`` 。


查看 Block 销售白名单注册是否还在进行中
_________________________________________________________________

.. code-block:: text

   // solidity

   function allowWhitelistRegistration() public view returns (bool) {
       return _allowWhitelistRegistration;
   }

.. code-block:: text

   // solidity

   function disableBlockSaleWhitelistRegistration() external onlyOwner {
       _allowWhitelistRegistration = false;
       emit BlockSaleWhitelistRegistrationDisabled();
   }

   执行合约中的功能函数 ``allowWhitelistRegistration()`` ，如果返回 ``true`` 说明注册是被允许的。

   一旦返回 ``false`` 就意味着白名单注册已经关闭，并且不可逆。

.. _whitelist_transfer_whitelist_qualification:

白名单资格支持过户
_____________________________________________

.. code-block:: text

   // solidity

   function transferWhitelist(address account) external onlyInWhitelist {
       require(isNotContract(account));
       _refCount[account] = _refCount[msg.sender];
       _refCount[msg.sender] = 0;
       _referrer[account] = _referrer[msg.sender];
       _referrer[msg.sender] = address(0);
       emit BlockSaleWhitelistTransferred(msg.sender, account);
   }

白名单资格支持过户
   只需执行合约中的功能函数 ``transferWhitelist(address account)`` ，如果你需要。

