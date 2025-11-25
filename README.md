# Carbon Footprint Calculator
This is an project that I made using an module in python called streamlit.
It's main functionality is to tell the user their total CO2 emissions per year based on their daily activities so that they become more surrounding conscious than they ever were.
**FEATURES**: User inputs their daily activities such as Transportation, Electricity, etc. and gets the total CO2 emission and suggetions as the output.
**TECHNOLOGIES/TOOLS USED**: The tools used in this project is an module in Python programming language called "Streamlit".
**STEPS TO INSTALL & RUN THE PROJECT**: It is advised that one should use VS Code for viewing this project and should download the streamlit module or package by putting exactly this in the terminal: python -m pip install streamlit
**INSTRUCTIONS FOR TESTING**: The user should follow the instructions above and put the Source Code below in VS Code and click the run icon.

Although the Source Code File is uploaded in this repository itself, it is also put here for further convinience.
**SOURCE CODE**:
import streamlit as st
EMISSIONFACTORS={"India":{
"Transportation": 0.20,
"Electricity": 0.76,
"Meals": 1.25,
"Waste": 0.52,
"Living Area": 0.8
},
"USA":{
"Transportation": 0.27,
"Electricity": 0.4,
"Meals": 2.25,
"Waste": 0.8,
"Living Area": 2    
},
"UK":{
"Transportation": 0.18,
"Electricity": 0.23,
"Meals": 1.8,
"Waste": 0.6,
"Living Area": 1.2    
}
}

st.set_page_config(layout="wide",
page_title="Carbon Footprint Calculator")
st.title("Carbon Footprint Calculator")

st.subheader("Your Country")
country=st.selectbox("Select",["India","USA","UK"])
col1,col2=st.columns(2)

with col1:
    st.subheader("Daily Commute Distance(in km)")
    distance=st.slider("Distance",0.0,200.0,key="distance_input")
                       
    st.subheader("Monthly Electricity Consumption(in kwh)")
    electricity=st.slider("Electricity",0.0,100.0,key="electricity_input")

    st.subheader("Your living area(in sq.ft)")
    living_area=st.slider("Living area",50.0,5000.0,key="livingarea_input")
                       
with col2:
    st.subheader("Waste generated per week(in kg)")
    waste=st.slider("Waste",0.0,100.0,key="waste_input")
                       
    st.subheader("Number of meals per day")
    meals=st.number_input("Meals",0,key="meals_input")

if distance >0:
    distance=distance*365

if electricity>0:
    electricity=electricity*12  

if living_area>0:
    living_area=living_area*12                                 

if meals>0:
    meals=meals*365

if waste >0:
    waste=waste*52

transport_emissions= EMISSIONFACTORS[country]['Transportation']*distance        
electricity_emissions= EMISSIONFACTORS[country]['Electricity']*electricity
living_area_emissions= EMISSIONFACTORS[country]['Living Area']*living_area
meals_emissions= EMISSIONFACTORS[country]['Meals']*meals
waste_emissions= EMISSIONFACTORS[country]['Waste']*waste

transport_emissions=round(transport_emissions/1000,2)
electricity_emissions=round(electricity_emissions/1000,2)
living_area_emissions=round(living_area_emissions/1000,2)
meals_emissions=round(meals_emissions/1000,2)
waste_emissions=round(waste_emissions/1000,2)

#converrt emissions to tonnes and round off to 2 decimals
total_emissions=round(
    transport_emissions+electricity_emissions+living_area_emissions+waste_emissions+meals_emissions,2
)

if st.button("Calculate CO2 Emissions"):
    st.header("Results")

    col3,col4=st.columns(2)

    with col3:
        st.subheader("Carbon Emission by Categories")
        st.info(f"Transportation: {transport_emissions} tonnes CO2 per year")
        st.info(f"Electricity: {electricity_emissions} tonnes CO2 per year")
        st.info(f"Living Area:{living_area_emissions} tonnes CO2 per year")
        st.info(f"Diet: {meals_emissions} tonnes CO2 per year")
        st.info(f"Waste: {waste_emissions} tonnes CO2 per year")

    with col4:
        st.subheader("Total Carbon Footprint")
        st.info(f"Your total Carbon Footprint is: {total_emissions} tonnes CO2 per year")
        st.subheader("Suggestions To Minimize CO2 Emmisions")
        st.warning("Reducing CO₂ emissions calls for the combined efforts from the people and governments; you should meaningfully lower your footprint by using cleaner transport, saving on electricity, choosing meals with more plants, and reducing waste. Although there is no strict 'ideal' level of CO₂ emissions rule set for individuals, the UN's Intergovernmental Panel on Climate Change (IPCC) has estimated that, for the whole world, average emissions need to be reduced to about 2 tonnes of CO₂ per person per year by 2030-2040 to keep global warming below 1.5°C. This value is not a rule but a scientific guideline derived from the carbon budget of the planet. The current emissions now vary widely from country to country. India emits about 2 tonnes per person per year, the U.K. about 5-6 tonnes, and the U.S. about 15-16 tonnes. These figures are the proof of how lifestyle, energy sources, and infrastructure can influence a country's footprint and how far many regions still are from the sustainable 2-tonne benchmark.")
