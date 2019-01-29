### farwestToken example

Need a general explanation of what this example does here, and explanations of each chunk of code below:

```
pragma solidity ^0.4.21;
// Abstract contract for the full ERC 20 Token standard
contract EIP20Interface {
uint256 public totalSupply;
function balanceOf(address _owner) public view returns (uint256 balance);
function transfer(address _to, uint256 _value) public returns (bool success);
function transferFrom(address _from, address _to, uint256 _value) public returns (bool
success);
function approve(address _spender, uint256 _value) public returns (bool success);
function allowance(address _owner, address _spender) public view returns (uint256
remaining);
event Transfer(address indexed _from, address indexed _to, uint256 _value);
event Approval(address indexed _owner, address indexed _spender, uint256 _value);
}
```

### farwestToken example: constructor definition
```
contract EIP20 is EIP20Interface {
uint256 constant private MAX_UINT256 = 2**256 - 1;
mapping (address => uint256) public balances;
mapping (address => mapping (address => uint256)) public allowed;

string public name;
uint8 public decimals;
string public symbol;

constructor (
uint256 _initialAmount,
string _tokenName,
uint8 _decimalUnits,
string _tokenSymbol
) 
public {
balances[msg.sender] = _initialAmount;
totalSupply = _initialAmount;
name = _tokenName;
decimals = _decimalUnits;
symbol = _tokenSymbol;
}
```

### farwestToken example: transfer function definition

```
function transfer(address _to, uint256 _value) public returns (bool success) {
require(balances[msg.sender] >= _value);
balances[msg.sender] -= _value;
balances[_to] += _value;
emit Transfer(msg.sender, _to, _value);
return true;
}

function transferFrom(address _from, address _to, uint256 _value) public returns (bool success) {
uint256 allowance = allowed[_from][msg.sender];
require(balances[_from] >= _value && allowance >= _value);
balances[_to] += _value;
balances[_from] -= _value;
if (allowance < MAX_UINT256) {
allowed[_from][msg.sender] -= _value;
}
emit Transfer(_from, _to, _value);
return true;
}
```

### farwestToken example: balance etc functions

```
function balanceOf(address _owner) public view returns (uint256 balance) {
return balances[_owner];
}
function approve(address _spender, uint256 _value) public returns (bool
success) {
allowed[msg.sender][_spender] = _value;
emit Approval(msg.sender, _spender, _value);
return true;
}
function allowance(address _owner, address _spender) public view returns
(uint256 remaining) {
return allowed[_owner][_spender];
}
```

### farwestToken example: main class definition

```
contract FarwestToken is EIP20 {
string public constant name = "FarwestToken";
string public constant symbol = "FWT";
uint8 public constant decimals = 18;
uint256 initialSupply = 210000000000 * 10 ** uint256(decimals);
address owner;
constructor () EIP20 (initialSupply, name, decimals, symbol) public {
owner = msg.sender;
}
function mintToken(address recipient, uint amount) public {
require (msg.sender == owner);
balances[recipient] += amount;
totalSupply += amount;
emit Transfer(0, this, amount);
emit Transfer(this, recipient, amount);
}
```

### farwestToken example: gateway definition

```
function () public payable {
address recipient = msg.sender;
uint256 getTokens = 1000 * msg.value; // 1:1000 to get tokens,
msg.value is the received ether
balances[recipient] += getTokens;
balances[owner] -= getTokens;
emit Transfer(owner, recipient, getTokens);
owner.transfer(msg.value);
} 
```

### Compile and Deploy farwestToken: Prepare the following
• A working Wanchain client node, see previous section
• Remix online or remix standalone IDE
• A smart contract such as farwestToken.sol

### Compile and Deploy farwestToken:
• Go to remix, copy and paste your smart contract code, make static
syntax analysis, and compile it
• Click Details on the right panel of remix, copy all the code of
WEB3DEPLOY section from the pop-up
• Copy the script and run it in gwan console