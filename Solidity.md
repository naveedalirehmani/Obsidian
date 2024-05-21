
### Functions
![[Pasted image 20240508151837.png]]

### Maps
maps are similar to objects in javascript.
![[Pasted image 20240509153514.png]]


### Arrays
![[Pasted image 20240509154753.png]]

### Visibilities

1. **External**: They can be called by other contracts or transactions and cannot be accessed internally
2. **Internal**: they can only be called within the contract that defines them and any derived contracts. They are not accessible by contracts that inherit from them or by external contracts.
3. **Private**: Private functions and state variables are only accessible within the contract that defines them. They are not accessible by derived contracts or external contracts.
4. **Public**: Public functions and state variables can be accessed both internally and externally.
  
| Visibility Specifier | Accessible in Derived Class | Accessible from Outside | Accessible for Another Contract | callable within contract |     |
| -------------------- | --------------------------- | ----------------------- | ------------------------------- | ------------------------ | --- |
| external             | Yes                         | Yes                     | yes                             | No                       |     |
| public               | Yes                         | Yes                     | Yes                             | Yes                      |     |
| private              | No                          | No                      | No                              | Yes                      |     |
| internal             | Yes                         | No                      | No                              | Yes                      |     |
	