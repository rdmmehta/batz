---
layout: page
title: Fixed Deposit Interest Calculator
permalink: /fd-interest-calculator
comments: false
---

use the form below to calculate Fixed Deposit Interest.
  

<div id="root"></div>

<script>
const { useState, useEffect } = React

const App = () => {
  
  const [principal, setPrincipal] = useState(0.00);
  const [years, setYears] = useState(0.00);
  const [interestRate, setInterestRate] = useState(0.00);
  const [compoundFrequency, setCompoundFrequency] = useState(1.00);
  const [final, setFinal] = useState(0.00);
  
  const calculate = () => {
    let finalAmount = principal * (Math.pow((1 + (interestRate/100 * compoundFrequency)), (years / compoundFrequency) ))
    setFinal(finalAmount.toFixed(2))
  }
  
  useEffect(calculate, [principal, interestRate, compoundFrequency, years])
  
  const handleCompoundSelect = ({ target: { value } }) => setCompoundFrequency(value)
  
  const handleChange = (event) => {
    const { target: { name, value } } = event
    switch (name) {
      case "principal":
        setPrincipal(value); break;
      case "years":
        setYears(value); break;
      case "interestRate":
        setInterestRate(value); break;
      default: break;
    }
  };

  return (
    <div className="box">      
      <h1>
        Compound Interest Calculator
      </h1>
      <form className="form">
        <div class="field">
          <label for="principal">Principal Amount ($)</label>
          <input type="number" value={principal} name="principal" class="input" onChange={handleChange}/>
        </div>
        <div class="field">
          <label for="years">Number of Years</label>
          <input type="number" value={years} name="years" class="input" onChange={handleChange}/>
        </div>
        <div class="control field" has-icons-right>
          <label for="interestRate">Interest Rate (%)</label>
          <input type="number" value={interestRate} name="interestRate"  class="input" onChange={handleChange}/>
        </div>
        <div class="field">
          <label for="period">Compounding Frequency</label>
          <br/>
          <div class="select">
            <select value={compoundFrequency} onChange={handleCompoundSelect}>
              <option value={1/4}>Yearly</option>
              <option value={1/12}>Monthly</option>
              <option value={1/4}>Quarterly</option>
              <option value={1/365}>Daily</option>
            </select>
          </div>
        </div>
        <div class="field">
          <label for="final">Final Amount ($)</label>
          <input type="number" value={final} name="final"  class="input" disabled/>
        </div>
      </form>
    </div>
  )
}

ReactDOM.render(<App />, document.getElementById("root"))
</script>

<script. src="https://cdnjs.cloudflare.com/ajax/libs/react/16.13.1/umd/react.production.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/react-dom/16.13.1/umd/react-dom.production.min.js"></script>


