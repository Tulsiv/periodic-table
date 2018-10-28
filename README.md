# periodic-table
package com.kmit.pt1;


import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.amazon.speech.json.SpeechletRequestEnvelope;
import com.amazon.speech.slu.Intent;
import com.amazon.speech.slu.Slot;
import com.amazon.speech.speechlet.IntentRequest;
import com.amazon.speech.speechlet.LaunchRequest;
import com.amazon.speech.speechlet.Session;
import com.amazon.speech.speechlet.SessionEndedRequest;
import com.amazon.speech.speechlet.SessionStartedRequest;
import com.amazon.speech.speechlet.SpeechletResponse;
import com.amazon.speech.speechlet.SpeechletV2;
import com.amazon.speech.ui.PlainTextOutputSpeech;
import com.amazon.speech.ui.Reprompt;
import com.amazon.speech.ui.SimpleCard;



/**
* This sample shows how to create a Lambda function for handling Alexa Skill requests that:
 * @author tele
 *
 */
public class pt1ServiceSpeechlet implements SpeechletV2 {
private static final Logger log = LoggerFactory.getLogger(pt1ServiceSpeechlet.class);

@Override
public void onSessionStarted(SpeechletRequestEnvelope<SessionStartedRequest> requestEnvelope) {
    log.info("onSessionStarted requestId={}, sessionId={}", requestEnvelope.getRequest().getRequestId(),
            requestEnvelope.getSession().getSessionId());

    // any initialization logic goes here
}

@Override
public SpeechletResponse onLaunch(SpeechletRequestEnvelope<LaunchRequest> requestEnvelope) {
    log.info("onLaunch requestId={}, sessionId={}", requestEnvelope.getRequest().getRequestId(),
            requestEnvelope.getSession().getSessionId());

    String speechOutput =
       "Welcome to Alexa Periodic Table Skill. You can ask me various details like Atomic mass, Atomic number, Latin name, Position,Type and Physical state of the Element";
    // If the user either does not reply to the welcome message or says
    // something that is not understood, they will be prompted again with this text.
    String repromptText = "For instructions on what you can say, please say help me.";

    // Here we are prompting the user for input
    return newAskResponse(speechOutput, repromptText);
    
}

@Override
public SpeechletResponse onIntent(SpeechletRequestEnvelope<IntentRequest> requestEnvelope) {
    IntentRequest request = requestEnvelope.getRequest();
    Session session = requestEnvelope.getSession();
    log.info("onIntent requestId={}, sessionId={}", request.getRequestId(),
            requestEnvelope.getSession().getSessionId());

    Intent intent = request.getIntent();
    String intentName = (intent != null) ? intent.getName() : null;

    if ("pt".equals(intentName)) {
        return getHelloWorldIntent(intent,session);
    } else if ("AMAZON.HelpIntent".equals(intentName)) {
        return getHelp();
    } else if ("AMAZON.StopIntent".equals(intentName)) {
        PlainTextOutputSpeech outputSpeech = new PlainTextOutputSpeech();
        outputSpeech.setText("Goodbye");

        return SpeechletResponse.newTellResponse(outputSpeech);
    } else if ("AMAZON.CancelIntent".equals(intentName)) {
        PlainTextOutputSpeech outputSpeech = new PlainTextOutputSpeech();
        outputSpeech.setText("Goodbye");

        return SpeechletResponse.newTellResponse(outputSpeech);
    } else {
        String errorSpeech = "This is unsupported.  Please try something else.";
        return newAskResponse(errorSpeech, errorSpeech);
    }
}

@Override
public void onSessionEnded(SpeechletRequestEnvelope<SessionEndedRequest> requestEnvelope) {
    log.info("onSessionEnded requestId={}, sessionId={}", requestEnvelope.getRequest().getRequestId(),
            requestEnvelope.getSession().getSessionId());

    // any cleanup logic goes here
}

/**
 * Creates a {@code SpeechletResponse} for the RecipeIntent.
 *
 * @param intent
 *            intent for the request
 * @return SpeechletResponse spoken and visual response for the given intent
 */
private SpeechletResponse getHelloWorldIntent(Intent intent,Session session) {
        
        
	int atomicno[]= {1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,101,102,103,104,105,106,107,108,109,110,111,112,113,114,115,116,117,118};
    double atomicwt[]= {1.008,4.003,6.941,9.0121,10.811,12.011,14.007,15.999,18.998,20.180,22.990,24.305,26.982,28.086,30.914,32.066,35.453,39.948,39.098,40.078,44.956,47.867,50.942,51.996,54.938,55.845,58.933,58.693,63.546,65.39,69.723,72.61,74.922,78.96,79.904,83.30,
    		85.468,87.62,88.906,91.224,92.906,95.94,98,101.07,102.906,106.42,107.868,112.411,114.818,118.710,121.760,126.904,127.6,131.29,132.905,137.327,138.906,140.116,140.908,144.908,145,150.36,151.25,157.25,158.925,162.50,164.930,167.26,168.934,173.04,174.967,178.49,180.948,183.84,186.207,190.23,192.217,195.078,196.967,200.59,204.383,207.2,208.980,209,210,222,223,226,227,232.038,231.036,238.029,237,244,243,247,247,251,252,257,258,259,262,261,262,263,262,265,266,269,272,285,284,289,288,292,000,294};
    String name[]= {"Hydrogen","Helium","Lithium","Beryllium","Boron","Carbon","Nitrogen","Oxygen","Fluorine","Neon","Sodium","Magnesium","Aluminium","Silicon",
    		"Phosphorus","Sulphur","Chlorine","Argon","Potassium","Calcium","Scandium","Titanium","Vanadium","Chromium","Manganese","Iron","Cobalt","Nickel","Copper","Zinc","Gallium","Germanium","Arsenic","Selenium","Bromine",
    		"Krypton","Rubidium","Strontium","Yttrium","Zirconium","Niobium","Molybdenum","Technetium","Ruthenium","Rhodium","Palladium","Silver","Cadmium","Indium","Tin","Antimony","Tellurium","Iodine","Xenon","Cesium","Barium",
    		"Lanthanium","Cerium","Praseodymium","Neodynium","Promethium","Samarium","Europium","Gadolinium","Terbium","Dysprosium","Holmium","Erbium","Thulium","Ytterbium","Lutetium","Hafnium","Tantalum","Tungsten","Rhenium","Osmium","Iridium","Platinum",
    		"Gold","Mercury","Thallium","Lead","Bismuth","Polonium","Astatine","Radon","Francium","Radium","Actinium","Thorium","Protactinium","Uranium","Neptunium","Plutonium","Americium","Curium","Berkelium","Californium","Einsteinium","Fermium","Mendelevium","Nobelium","Lawrencium",
    		"Rutherfordium","Dubnium","Seaborgium","Bohrium","Hassium","Meiternium","Darmstadtium","Rontgentium","Copernicium","Nihonium","Flerovium","Moscovium","Livermorium","Tennessine","Oganesson"};
    String symbol[]= {"H","He","Li","Be","B","C","N","O","F","Ne","Na","Mg","Al","Si","P","S","Cl","Ar","K","Ca","Sc","Ti","V","Cr","Mn","Fe","Co","Ni","Cu","Zn","Ga","Ge","As","Se","Br","Kr","Rb","Sr","Y","Zr","Nb","Mo","Tc","Ru","Rh","Pd","Ag","Cd","In","Sn","Sb","Te","I","Xe","Cs","Ba","La",
    		"Ce","Pr","Nd","Pm","Sm","Eu","Gd","Tb","Dy","Ho","Er","Tm","Yb","Lu","Hf","Ta","W","Re","Os","Ir","Pt","Au","Hg","Tl","Pb","Bi","Po","At","Rn","Fr","Ra","Ac","Th","Pa","U","Np","Pu","Am","Cm","Bk","Cf","Es","Fm","Md","No","Lr","Rf","Db","Sg","Bh","Hs","Mt","Ds","Rg","Cn","Nh","Fl","Mc","Lv","Ts","Og"};
    String latinname[]= {"Hydrogen","Helium","Lithium","Beryllium","Boron","Carbon","Nitrogen","Oxygen","Fluorine","Neon","Natrium","Magnesium","Aluminium","Silicon",
    		"Phosphorus","Sulphur","Chlorine","Argon","Kalium","Calcium","Scandium","Titanium","Vanadium","Chromium","Manganese","Ferrum","Cobalt","Nickel","Cuprum","Zinc","Gallium","Germanium","Arsenic","Selenium","Bromine",
    		"Krypton","Rubidium","Strontium","Yttrium","Zirconium","Niobium","Molybdenum","Technetium","Ruthenium","Rhodium","Palladium","Argentum","Cadmium","Indium","Stannum","Stibium","Tellurium","Iodine","Xenon","Cesium","Barium",
    		"Lanthanium","Cerium","Praseodymium","Neodynium","Promethium","Samarium","Europium","Gadolinium","Terbium","Dysprosium","Holmium","Erbium","Thulium","Ytterbium","Lutetium","Hafnium","Tantalum","Wolfram","Rhenium","Osmium","Iridium","Platinum",
    		"Aurum","Hydragyrum","Thallium","Plumbum","Bismuth","Polonium","Astatine","Radon","Francium","Radium","Actinium","Thorium","Protactinium","Uranium","Neptunium","Plutonium","Americium","Curium","Berkelium","Californium","Einsteinium","Fermium","Mendelevium","Nobelium","Lawrencium",
    		"Rutherfordium","Dubnium","Seaborgium","Bohrium","Hassium","Meiternium","Darmstadtium","Rontgentium","Ununbium","Ununtrium","Ununquadrium","Ununpentium","Ununhexium","null","Ununoctium"};
    String type[]= {"Non Metal","Non Metal","Metal","Metal","Metalloid","Non Metal","Non Metal","Non Metal","Non Metal","Non Metal","Metal","Metal","Metal","Metalloid","Non Metal","Non Metal","Non Metal","Non Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metalloid","Metalloid","Non Metal","Non Metal","Non Metal"
    		,"Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metalloid","Metalloid","Non Metal","Non Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metalloid","Metalloid","Non Metal"
    		,"Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Metal","Not defined","Non metal"};
    String location[]= {"Period 1 Group 1A","Period 1 Group 0","Period 2 Group 1A","Period 2 Group 2A","Period 2 Group 3A","Period 2 Group 4A","Period 2 Group 5A","Period 2 Group 6A","Period 2 Group 7A","Period 2 Group 0","Period 3 Group 1A","Period 3 Group 2A","Period 3 Group 3A","Period 3 Group 4A","Period 3 Group 5A","Period 3 Group 6A","Period 3 Group 7A","Period 3 Group 0","Period 4 Group 1A","Period 4 Group 2A","Period 4 Group 3B","Period 4 Group 4B","Period 4 Group 5B","Period 4 Group 6B","Period 4 Group 7B","Period 4 Group 8B","Period 4 Group 8B","Period 4 Group 8B","Period 4 Group 1B","Period 4 Group 2B"
    		,"Period 4 Group 3A","Period 4 Group 4A","Period 4 Group 5A","Period 4 Group 6A","Period 4 Group 7A","Period 4 Group 0","Period 5 Group 1A","Period 5 Group 2A","Period 5 Group 3B","Period 5 Group 4B","Period 5 Group 5B","Period 5 Group 6B","Period 5 Group 7B","Period 5 Group 8B","Period 5 Group 8B","Period 5 Group 8B","Period 5 Group 1B","Period 5 Group 2B","Period 5 Group 3A","Period 5 Group 4A","Period 5 Group 5A","Period 5 Group 6A","Period 5 Group 7A","Period 5 Group 0","Period 6 Group 1A","Period 6 Group 2A","Period 6 Group 3B","Period 6 Group 3B","Period 6 Group 3B","Period 6 Group 3B","Period 6 Group 3B","Period 6 Group 3B","Period 6 Group 3B","Period 6 Group 3B","Period 6 Group 3B","Period 6 Group 3B","Period 6 Group 3B","Period 6 Group 3B","Period 6 Group 3B","Period 6 Group 3B","Period 6 Group 3B",
    		"Period 6 Group 4B","Period 6 Group 5B","Period 6 Group 6B","Period 6 Group 7B","Period 6 Group 8B","Period 6 Group 8B","Period 6 Group 8B","Period 6 Group 1B","Period 6 Group 2B","Period 6 Group 3A","Period 6 Group 4A","Period 6 Group 5A","Period 6 Group 6A","Period 6 Group 7A","Period 6 Group 0","Period 7 Group 1A","Period 7 Group 2A","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 3B","Period 7 Group 4B","Period 7 Group 5B","Period 7 Group 6B","Period 7 Group 7B","Period 7 Group 8B","Period 7 Group 8B","Period 7 Group 8B","Period 7 Group 1B","Period 7 Group 2B","Period 7 Group 3A","Period 7 Group 4A","Period 7 Group 5A","Period 7 Group 6A","Period 7 Group 7A","Period 7 Group 0"};
	String state[]= {"Gas","Gas","Solid","Solid","Solid","Solid","Gas","Gas","Gas","Gas","Solid","Solid","Solid","Solid","Solid","Solid","Gas","Gas","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Liquid","Gas","Solid","Solid","Solid","Solid","Solid","Solid","Not found in Nature","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Gas"
			,"Solid","Solid","Solid","Solid","Solid","Solid","Not found in Nature","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Solid","Liquid","Solid","Solid","Solid","Solid","Solid","Gas","Solid","Solid","Solid","Solid","Solid","Solid","Not found in Nature","Solid","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature","Not found in Nature"};
    
    Slot nameSlot = intent.getSlot("question");
	 
    //session.setAttribute(e_key, nameSlot.getValue());
    String a=nameSlot.getValue();
    Slot nameSlot1 = intent.getSlot("element");
	 
    //session.setAttribute(e_key, nameSlota.getValue());
    String value=nameSlot1.getValue();
    String resString="";
    
	
        int i,j=-1;
        for(i=0;i<atomicno.length;i++)
        {
        	if(name[i].equalsIgnoreCase(value))
        	{   
        	j=i;
        		break;
        	}
    
        }
        
        if(j>=0)
        {
        switch(a)
        { case "atomicno":
        case "atomic number":
        	resString="The atomic number is "+atomicno[j];
        	break;
        case "atomicwt":
        case "atomic weight":
        case "atomic mass":
        	resString="The atomic weight is "+atomicwt[j];
        	break;
        case "symbol":
        	resString="The symbol is "+symbol[j];
        	break;
        case "latinname":
        case "latin name":
        case "other name":
        	resString="The latin name is "+latinname[j];
        	break;
        case "type":
        case "kind":
        	resString="The elemental type is "+type[j];
        	break;
        case "position":
        case "location":
        	resString="The position of "+value+" is"+location[j];
        	break;
        case "form":
        case "state":
        	resString="The Physical State of "+value+" is "+state[j];
        	break;
        case "details":
        case "info":
        case "characteristics":
        case "information":
        	resString="The features of "+value+" are \n"+
        "Atomic mass="+atomicwt[j]+
        "\n Atomic number="+atomicno[j]+
        "\n Symbol="+symbol[j]+
        "\n Latin name="+latinname[j]+
        "\n Position of the Element is "+location[j]+
        "\n Type of element="+type[j]+
        "\n Physical State of the element="+state[j];
        	break;
        		
        	default: resString="Sorry please check your input";break;
        }}
        else
        {
        	resString="Please check your input";
        }
        String responseText = resString;

        
        PlainTextOutputSpeech outputSpeech = new PlainTextOutputSpeech();
        outputSpeech.setText(responseText);

        SimpleCard card = new SimpleCard();
        card.setTitle("Intent Values  ");
        card.setContent(responseText);
        
        PlainTextOutputSpeech repromptOutputSpeech = new PlainTextOutputSpeech();
        repromptOutputSpeech.setText(responseText);
        Reprompt reprompt = new Reprompt();
        reprompt.setOutputSpeech(repromptOutputSpeech);
        
        return SpeechletResponse.newAskResponse(outputSpeech,reprompt, card);
    
        
   
     
}

/**
 * Creates a {@code SpeechletResponse} for the HelpIntent.
 *
 * @return SpeechletResponse spoken and visual response for the given intent
 */
private SpeechletResponse getHelp() {
    String speechOutput =
            "You can say wish my friend";
    String repromptText =
    		"You can say wish my friend";
    return newAskResponse(speechOutput, repromptText);
}

/**
 * Wrapper for creating the Ask response. The OutputSpeech and {@link Reprompt} objects are
 * created from the input strings.
 *
 * @param stringOutput
 *            the output to be spoken
 * @param repromptText
 *            the reprompt for if the user doesn't reply or is misunderstood.
 * @return SpeechletResponse the speechlet response
 */
private SpeechletResponse newAskResponse(String stringOutput, String repromptText) {
	
	 SimpleCard card = new SimpleCard();
     card.setTitle(stringOutput);
    PlainTextOutputSpeech outputSpeech = new PlainTextOutputSpeech();
    outputSpeech.setText(stringOutput);

    PlainTextOutputSpeech repromptOutputSpeech = new PlainTextOutputSpeech();
    repromptOutputSpeech.setText(repromptText);
    Reprompt reprompt = new Reprompt();
    reprompt.setOutputSpeech(repromptOutputSpeech);

    return SpeechletResponse.newAskResponse(outputSpeech, reprompt,card);
}



}
