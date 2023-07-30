<h2>1. In the title of the header, it displays 5 orders but there are 6 orders in the table. We want to display the total number of orders in the header title.</h2>
<p>
<HeaderTitle primaryTitle="Orders" secondaryTitle="6 orders" />
</p>
<h4>Before it was 5 order in Dashboard.jsx</h4>


<h2>2. In the table order submitted date is missing, we have timestamp data included in the src\assets\timeStamps.json with the corresponding ids, please combine that with the order data and make sure the order submitted date is being displayed in the table</h2>
<h4>
i copy the timestamp object from timeStamps.json and paste into data.json result object <h4>
<p>
"timestamps": {
        "orderReceived": "2022-11-04T15:29:00Z",
        "orderStatusUpdated": "2022-11-04T15:29:00Z",
        "orderSubmitted": "2022-11-04T15:29:00Z"
      }
</p>
<h2>3. Order Volume cell is displaying USD values, can you please make it display the currency value selected on the dropdown located in the header of the dashboard</h2>
<h4>
sol.
I pass the currency as a prop from Dashboard.jsx to List.jsx
</h4>
<p>
<List rows={mockData.results} currency={currency} />
</p>

<p>
const List = ({ rows ,currency}) => {
  return (
    <table className={styles.container}>
      <thead>
        <ListHeader>
          <ListHeaderCell>Order ID</ListHeaderCell>
          <ListHeaderCell>Buy/Sell</ListHeaderCell>
          <ListHeaderCell>Country</ListHeaderCell>
          <ListHeaderCell>Order Submitted</ListHeaderCell>
        <ListHeaderCell>Order Volume / {currency}</ListHeaderCell>  // here i am set the currency replce with USD
        </ListHeader>
      </thead>
      <tbody>
        {rows.map((row) => (
          <ListRow>
            <ListRowCell>{row["&id"]}</ListRowCell>
            <ListRowCell>{row.executionDetails.buySellIndicator}</ListRowCell>
            <ListRowCell>{row.executionDetails.orderStatus}</ListRowCell>
            <ListRowCell>{row.timestamps.orderSubmitted}</ListRowCell>
            <ListRowCell>{row.bestExecutionData.orderVolume[currency]}</ListRowCell> // previously here .USD but i use currency as a value.
          </ListRow>
        ))}
      </tbody>
    </table>
  );
};
</p>

<h2>5. Please clear the console errors and warnings.</h2>
<p>
  sol. 
    {Object.entries(cardData).map(([k, v],index) => (
        <div className={styles.cell} key={index}>
 </p>       
    <h4>Here i pass the index for unique key</h4>

<h2>6. When user selects an order, can you populate the Card on top of the listing component as shown in the image.</h2>
    sol.
   <p> <List rows={mockData.results} currency={currency} setSelectedOrderDetails={setSelectedOrderDetails} setSelectedOrderTimeStamps={setSelectedOrderTimeStamps}/>
   </p>
   <h4> Here I pass the setSelectedOrderTimeStamps and setSelectedOrderDetails as prop to List</h4>
   <h3>Then In List</h3>
   <p>
        {rows.map((row,index) => (
          <ListRow key={index} onClick={()=>{
            setSelectedOrderDetails(row.executionDetails);
            setSelectedOrderTimeStamps(row.timestamps);
          }}>
   </p>
   <h3>On each ListRow i add onClick function and set the value</h3>
