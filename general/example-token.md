---
description: >-
  The code of the IBEP20, IPantosInterface, PantosBaseToken and a reference
  implementation
---

# Example Token

### IBEP20

The IBEP20 interface is a set of standardized functions and events that must be implemented by token contracts to be compatible with the Pantos Digital Asset Standard (PANDAS). It inherits from the ERC20 token standard, ensuring compatibility with various blockchain ecosystems.&#x20;

```solidity
// SPDX-License-Identifier: Apache-2.0
pragma solidity >=0.8.0 <0.9.0;
pragma abicoder v2;

import "@openzeppelin/contracts/token/ERC20/IERC20.sol";

/**
 * @title BEP20 token interface
 */
interface IBEP20 is IERC20 {
    /**
     * @return The token decimals.
     */
    function decimals() external view returns (uint8);

    /**
     * @return The token symbol.
     */
    function symbol() external view returns (string memory);

    /**
     * @return The token name.
     */
    function name() external view returns (string memory);

    /**
     * @return The token owner.
     */
    function getOwner() external view returns (address);
}
```

### IPantosInterface

The IPantosToken interface is a set of standardized functions and events that must be implemented by token contracts to be compatible with the Pantos Digital Asset Standard (PANDAS). It inherits from the ERC20 token standard, ensuring compatibility with various blockchain ecosystems. The interface defines additional functions and events specifically tailored for cross-chain functionality, such as pantosTransfer, pantosTransferFrom, pantosTransferTo, and getPantosForwarder. By implementing this interface, token contracts can utilize Pantos Hub's cross-chain functionality.

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity >=0.8.0 <0.9.0;
pragma abicoder v2;
import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
import "./IBEP20.sol";
/**
 * @title Pantos token interface
 */
interface IPantosToken is IERC20, IBEP20 {
    event PantosForwarderSet(address pantosForwarder);
    event PantosForwarderUnset();
    // Only callable by the trusted Pantos forwarder
    function pantosTransfer(address sender, address recipient, uint256 amount)
        external;
    // Only callable by the trusted Pantos forwarder
    function pantosTransferFrom(address sender, uint256 amount) external;
    // Only callable by the trusted Pantos forwarder
    function pantosTransferTo(address recipient, uint256 amount) external;
    function getPantosForwarder() external view returns (address);
}
```

### PantosBaseToken

The PantosBaseToken is a base token contract that implements the IPantosToken interface, providing a foundation for creating custom tokens that are compatible with the Pantos Digital Asset Standard (PANDAS). This base contract ensures that the necessary functions and events for cross-chain functionality are implemented correctly, simplifying the process of creating new tokens. Developers can inherit from PantosBaseToken and extend it with their custom logic to create a new token that is compatible with Pantos Hub and can be transferred between various blockchains seamlessly.

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity >=0.8.0 <0.9.0;
pragma abicoder v2;
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "../interfaces/IPantosToken.sol";
/**
 * @title Pantos base token
 */
abstract contract PantosBaseToken is IPantosToken, ERC20, Ownable {
    uint8 private _decimals;
    address private _pantosForwarder;
    constructor(string memory name_, string memory symbol_, uint8 decimals_)
        ERC20(name_, symbol_)
    {
        _decimals = decimals_;
    }
    modifier onlyPantosForwarder() virtual {
        require(
            _pantosForwarder != address(0),
            "PantosBaseToken: PantosForwarder has not been set"
        );
        require(
            msg.sender == _pantosForwarder,
            "PantosBaseToken: caller is not the PantosForwarder"
        );
        _;
    }
    /// @dev See {IPantosToken-pantosTransfer}.
    function pantosTransfer(address sender, address recipient, uint256 amount)
        public
        virtual
        override
        onlyPantosForwarder
    {
        _transfer(sender, recipient, amount);
    }
    /// @dev See {IPantosToken-pantosTransferFrom}.
    function pantosTransferFrom(address sender, uint256 amount)
        public
        virtual
        override
        onlyPantosForwarder
    {
        _burn(sender, amount);
    }
    /// @dev See {IPantosToken-pantosTransferTo}.
    function pantosTransferTo(address recipient, uint256 amount)
        public
        virtual
        override
        onlyPantosForwarder
    {
        _mint(recipient, amount);
    }
    /// @dev See {IBEP20-decimals} and {ERC20-decimals}.
    function decimals()
        public
        view
        virtual
        override(IBEP20, ERC20)
        returns (uint8)
    {
        return _decimals;
    }
    /// @dev See {IBEP20-symbol} and {ERC20-symbol}.
    function symbol()
        public
        view
        virtual
        override(IBEP20, ERC20)
        returns (string memory)
    {
        return ERC20.symbol();
    }
    /// @dev See {IBEP20-name} and {ERC20-name}.
    function name()
        public
        view
        virtual
        override(IBEP20, ERC20)
        returns (string memory)
    {
        return ERC20.name();
    }
    /// @dev See {IBEP20-getOwner} and {Ownable-owner}.
    function getOwner() public view virtual override returns (address) {
        return owner();
    }
    /// @dev See {IPantosToken-getPantosForwarder}.
    function getPantosForwarder()
        public
        view
        virtual
        override
        returns (address)
    {
        return _pantosForwarder;
    }
    function _setPantosForwarder(address pantosForwarder)
        internal
        virtual
        onlyOwner
    {
        require(
            pantosForwarder != address(0),
            "PantosBaseToken: PantosForwarder must not be the zero account"
        );
        _pantosForwarder = pantosForwarder;
        emit PantosForwarderSet(pantosForwarder);
    }
    function _unsetPantosForwarder()
        internal
        virtual
        onlyOwner
    {
        _pantosForwarder = address(0);
        emit PantosForwarderUnset();
    }
}
```

### Example Token inherit from PantosBaseToken

The Example Token is a custom token that inherits from the PantosBaseToken. It is designed to be compatible with the Pantos Digital Asset Standard (PANDAS), making it easy to transfer the token across different blockchains. The Example Token has a name, symbol, and decimals value, which are set in the contract.

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity >=0.8.0 <0.9.0;
pragma abicoder v2;

import "./PantosBaseToken.sol";
/**
 * @title Pantos-compatible Example Token
 */
contract MyToken is PantosBaseToken {
    string private constant _NAME = "MyToken";
    string private constant _SYMBOL = "MT";
    uint8 private constant _DECIMALS = 18;

    /// @dev msg.sender receives all existing tokens.
    constructor(uint256 initialSupply)
        PantosBaseToken(_NAME, _SYMBOL, _DECIMALS)
    {
        ERC20._mint(msg.sender, initialSupply);
        // Contract is paused until it is fully initialized
    }
    /// @dev See {PantosBaseToken-_setPantosForwarder}.
    function setPantosForwarder(address pantosForwarder)
        external
        onlyOwner
    {
        _setPantosForwarder(pantosForwarder);
    }
}
```
