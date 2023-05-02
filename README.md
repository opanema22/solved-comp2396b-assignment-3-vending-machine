Download Link: https://assignmentchef.com/product/solved-comp2396b-assignment-3-vending-machine
<br>
Consider a vending machine, which vends soft drinks, that accept coins only. The vending machine allows customers to insert coins, purchase a product and reject inserted coins. In this assignment, you need to build a system to simulate the operations of vending soft drinks in a vending machine. Please read this assignment sheet carefully before starting your work.

Typical vending machine consist of these components:

<ul>

 <li>A Coin Slot allows customers to insert coins into the machine. It also serves as temporality storage for inserted coins and accumulates the amount of face value.</li>

 <li>A button to reject all inserted coins.</li>

 <li>A Coin Changer stores coins for giving change. Change is the money that is returned to the customer who has paid for the product that costs less than the amount that the customer has given.</li>

 <li>A Soft Drink Slot holds the same products of soft drinks in a column. When a transaction is made, the slot will drop a can of drink into the dispenser.</li>

</ul>

Standard workflow for vending a soft drink in a vending machine is as follow:

<ol>

 <li>The customer inserts coins into the Coin Slot.</li>

 <li>The customer selects a product.</li>

 <li>If the customer has inserted enough amount of money for the product, the vending machine firstly drops the product and return change (if necessary). Then, all coins in the Coin Slot are moved to the Coin Changer.</li>

</ol>




<strong>Task:</strong> Implement this system. Below shows a simple run-down.

<table width="0">

 <tbody>

  <tr>

   <td width="79">Sample main</td>

   <td colspan="2" width="619"><strong>public</strong> <strong>class</strong> Main {<strong>  public</strong> <strong>static</strong> <strong>void</strong> main(String[] args) {     VendingMachine v = <strong>new</strong> VendingMachine();v.addCoinToCoinChanger(Integer.<em>valueOf</em>(2));v.addCoinToCoinChanger(Integer.<em>valueOf</em>(2));v.addCoinToCoinChanger(Integer.<em>valueOf</em>(1));v.addSoftDrinkSlot(<strong>new</strong> SoftDrinkSlot(“Cocacola”, 4, 1)); // Price: $4, Quantity: 1v.addSoftDrinkSlot(<strong>new</strong> SoftDrinkSlot(“Pepsi”, 5, 3)); // Price: $5, Quantity: 3System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdInsertCoin()).execute(v, “10”));System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdInsertCoin()).execute(v, “2”));     System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdRejectCoins()).execute(v, “”));     System.<strong><em>out</em></strong>.println();System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdRejectCoins()).execute(v, “”));     System.<strong><em>out</em></strong>.println();System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdInsertCoin()).execute(v, “5”));System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdPurchase()).execute(v, “Pepsi”));     System.<strong><em>out</em></strong>.println();System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdInsertCoin()).execute(v, “10”));System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdInsertCoin()).execute(v, “5”));System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdPurchase()).execute(v, “Pepsi”));     System.<strong><em>out</em></strong>.println();System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdInsertCoin()).execute(v, “5”));System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdInsertCoin()).execute(v, “2”));System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdPurchase()).execute(v, “Pepsi”));     System.<strong><em>out</em></strong>.println();System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdRejectCoins()).execute(v, “”));System.<strong><em>out</em></strong>.println();System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdInsertCoin()).execute(v, “2”));System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdPurchase()).execute(v, “Pepsi”));     System.<strong><em>out</em></strong>.println();System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdInsertCoin()).execute(v, “2”));System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdPurchase()).execute(v, “Cocacola”));System.<strong><em>out</em></strong>.println();System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdInsertCoin()).execute(v, “2”));System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdInsertCoin()).execute(v, “2”));System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdPurchase()).execute(v, “Cocacola”));     System.<strong><em>out</em></strong>.println(((Command) <strong>new</strong> CmdRejectCoins()).execute(v, “”));   }} </td>

  </tr>

  <tr>

   <td width="79">Sample output</td>

   <td width="388">Inserted a $10 coin. $10 in Total.Inserted a $2 coin. $12 in Total.Rejected $2, $10. $12 in Total. Rejected no coin! Inserted a $5 coin. $5 in Total.Purchasing Pepsi… Success! Paid $5. No change. Inserted a $10 coin. $10 in Total.Inserted a $5 coin. $15 in Total.Purchasing Pepsi… Success! Paid $15. Change: $1, $2, $2, $5. Inserted a $5 coin. $5 in Total.Inserted a $2 coin. $7 in Total.Purchasing Pepsi… Insufficient change! Rejected $2, $5. $7 in Total. Inserted a $2 coin. $2 in Total.Purchasing Pepsi… Insufficient amount! Inserted $2 but needs $5. Inserted a $2 coin. $4 in Total.Purchasing Cocacola… Success! Paid $4. No change. Inserted a $2 coin. $2 in Total.Inserted a $2 coin. $4 in Total.Purchasing Cocacola… Out of stock!Rejected $2, $2. $4 in Total.<strong> </strong></td>

   <td width="231"></td>

  </tr>

 </tbody>

</table>







A partial completed VendingMachine class is provided as follows

<table width="0">

 <tbody>

  <tr>

   <td width="697"><strong>import</strong> java.util.ArrayList; <strong>public</strong> <strong>class</strong> VendingMachine {<strong>private</strong> ArrayList&lt;Integer&gt; coinChanger;  <strong>private</strong> ArrayList&lt;Integer&gt; coinSlot;<strong>private</strong> ArrayList&lt;SoftDrinkSlot&gt; softDrinkSlots; <strong>public</strong> VendingMachine() {         coinChanger = <strong>new</strong> ArrayList&lt;Integer&gt;();         coinSlot = <strong>new</strong> ArrayList&lt;Integer&gt;();softDrinkSlots = <strong>new</strong> ArrayList&lt;SoftDrinkSlot&gt;();} <strong>public</strong> <strong>void</strong> addCoinToCoinChanger(Integer c) {          coinChanger.add(c);} <strong>public</strong> <strong>void</strong> addSoftDrinkSlot(SoftDrinkSlot s) {                softDrinkSlots.add(s);}/* You may add other non-static properties and methods */} </td>

  </tr>

 </tbody>

</table>




You must not modify the parameter lists of the constructor, addCoinToCoinChanger() and addSoftDrinkSlot() as we will use these methods to initiate the vending machine in test cases evaluation.

The SoftDrinkSlot class is provided as follow

<table width="0">

 <tbody>

  <tr>

   <td width="697"><strong>public</strong> <strong>class</strong> SoftDrinkSlot { <strong>private</strong> String name;         <strong>private</strong> <strong>int</strong> price;<strong>private</strong> <strong>int</strong> quantity; <strong>public</strong> SoftDrinkSlot(String name, <strong>int</strong> price, <strong>int</strong> quantity) {<strong>this</strong>.name = name;            <strong>this</strong>.price = price;                <strong>this</strong>.quantity = quantity;}/* You may add other non-static properties and methods */} </td>

  </tr>

 </tbody>

</table>

You must not modify the parameter lists of the constructor as we will use it in test cases evaluation.

The system should be operated via commands (except initiating the vending machine), which is, every time we want to operate the vending machine, an instance of Command object should be created. The Command object will be the interface for the main program to perform actions on the Vending Machine. Different types of commands are handled by different specific classes that inherit the Command class. The Command class is defined as follows

<table width="0">

 <tbody>

  <tr>

   <td width="697"><strong>public</strong> <strong>class </strong>Command {     <strong>public</strong> String execute(VendingMachine v, String cmdPart){String result = null;<strong>return</strong> result;}}</td>

  </tr>

 </tbody>

</table>




You need to implement 3 commands for the system, namely CmdInsertCoin, CmdRejectCoins and CmdPurchase. These commands should inherit the Command class. Each Command class perform specific actions to the vending machine in the execute() method. The method takes the VendingMachine object and a command content in String as the input parameters. After performing actions, the method should return the result of the command in String.

<ol>

 <li>CmdInsertCoin – Insert a coin</li>

 <li>CmdRejectCoins – Reject all coins from Coin Slot</li>

 <li>CmdPurchase – Vend a can of soft drink to the customer. When giving a change to the customer, the machine should find the <strong>minimum number of coins</strong> in the Coin Changer to make the change.</li>

</ol>

For example, CmdInsertCoin inherit Command class and perform actions in the execute() method:

<strong>public</strong> <strong>class</strong> CmdInsertCoin <strong>extends </strong>Command {




@Override

<strong>public</strong> String execute(VendingMachine v, String cmdPart) {

Integer coin = Integer.<em>valueOf</em>(cmdPart);

// Add the coin to Coin Slot

<strong>return</strong> /*…*/;

}

}







You also need to add handling for the following special cases, but you can assume no more than one special case would happen simultaneously in our test cases.

<ul>

 <li>Insufficient amount of money to buy the drink.</li>

 <li>The drink is out of stock</li>

 <li>Not enough coins in Coin Changer for giving a particular amount of change to the customer.</li>

</ul>

<strong>Notes: </strong>

<ol>

 <li>The listing of coins should be sorted by the face value ascendingly.</li>

 <li>All coins are in dollar unit ($1, $2, $5, $10), no need to deal with cents.</li>

 <li>When preparing coins for a change, the vending machine looks for coins in the <strong>Coin Changer</strong></li>

 <li>The system should find the <strong>minimum number of coins</strong> for preparing the change. For example, if one $5 coin is available, then the $5 coin should be selected instead of selecting $1, $2 and $2 coins.</li>

 <li>You are free to add other classes that help you to implement the system. You can upload up to 50 files to Moodle.</li>

 <li>You must <strong>NOT</strong> declare any <strong>static variable</strong> in your program as a static variable will disrupt our evaluation system.</li>

 <li>If you failed to pass a test case, Moodle only shows you the last line of expected output and program output.</li>

</ol>