<template>
  <div class="skeleton">

    <header class="head">
        <div class="head__logo">
            <!--<img src="../assets/logo.png" alt="Logo">-->
        </div>
        <div class="head__export">
            <i class="fa fa-cloud-download fa-2x" aria-hidden="true"></i>
            <button @click="exportFunction()">Export</button>
        </div>
        <img class="head__avatar" src="../assets/elvis.jpg" alt="Avatar">
    </header>

    <div class="main_container">
        <nav>
            <div class="sections-menu">
                <ul>
                    <li>
                      <a href="">ΕΠΙΧΕΙΡΗΜΑΤΙΚΟ ΜΟΝΤΕΛΟ</a>
                      <ul>
                        <router-link to="/2a-identity" tag="li" class="">
                          <a>ΤΑΥΤΟΤΗΤΑ</a>
                        </router-link>
                        <router-link to="/2b-description" tag="li" class="">
                          <a>ΠΕΡΙΓΡΑΦΗ</a>
                        </router-link>
                      </ul>
                    </li>
                    <li>
                      <a href="">ΑΝΑΛΥΣΗ ΑΓΟΡΑΣ</a>
                      <ul>
                        <router-link to="/market-general" tag="li" class="">
                          <a>Γενικές</a>
                        </router-link>
                      </ul>
                    </li>
                    <!-- <li>
                        <a href="">ΕΠΙΧΕΙΡΗΜΑΤΙΚΟ ΜΟΝΤΕΛΟ</a>
                        <ul>
                            <li>
                                <a href="">ΤΑΥΤΟΤΗΤΑ</a>
                            </li>
                            <li>
                                <a href="">ΠΕΡΙΓΡΑΦΗ</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΑΝΘΡΩΠΙΝΟ ΔΥΝΑΜΙΚΟ</a>
                        <ul>
                            <li>
                                <a href="">ΟΜΑΔΑ ΔΙΟΙΚΗΣΗΣ</a>
                            </li>
                            <li>
                                <a href="">ΠΡΟΣΩΠΙΚΟ</a>
                            </li>
                            <li>
                                <a href="">ΕΞΩΤΕΡΙΚΟΙ ΣΥΝΕΡΓΑΤΕΣ</a>
                            </li>
                            <li>
                                <a href="">ΑΝΑΛΥΣΗ ΚΟΣΤΟΥΣ</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΕΓΚΑΤΑΣΤΑΣΕΙΣ - ΕΞΟΠΛΙΣΜΟΣ</a>
                        <ul>
                            <li>
                                <a href="">ΤΟΠΟΣ ΕΓΚΑΤΑΣΤΑΣΗΣ</a>
                            </li>
                            <li>
                                <a href="">ΕΞΟΠΛΙΣΜΟΣ</a>
                            </li>
                            <li>
                                <a href="">ΑΝΑΛΥΣΗ ΚΟΣΤΟΥΣ</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΠΡΟΪΟΝΤΑ - ΥΠΗΡΕΣΙΕΣ</a>
                        <ul>
                            <li>
                                <a href="">ΠΡΟΙΟΝΤΑ - ΥΠΗΡΕΣΙΕΣ</a>
                            </li>
                            <li>
                                <a href="">ΠΝΕΥΜΑΤΙΚΗ ΙΔΙΟΚΤΗΣΙΑ</a>
                            </li>
                            <li>
                                <a href="">ΑΝΑΛΥΣΗ ΕΣΟΔΩΝ</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΑΝΑΛΥΣΗ ΑΓΟΡΑΣ</a>
                        <ul>
                            <li>
                                <a href="">ΑΝΑΛΥΣΗ SWOT</a>
                            </li>
                            <li>
                                <a href="">ΑΝΑΛΥΣΗ PESTEL</a>
                            </li>
                            <li>
                                <a href="">ΓΕΝΙΚΕΣ ΠΑΡΑΤΗΡΗΣΕΙΣ</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΣΤΡΑΤΗΓΙΚΗ MARKETING</a>
                        <ul>
                            <li>
                                <a href="">ΣΤΡΑΤΗΓΙΚΗ</a>
                            </li>
                            <li>
                                <a href="">ΕΝΕΡΓΕΙΕΣ MARKETING</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΧΡΗΜΑΤΟΙΚΟΝΟΜΙΚΟΣ ΣΧΕΔΙΑΣΜΟΣ</a>
                        <ul>
                            <li>
                                <a href="">ΚΟΣΤΟΣ ΕΝΑΡΞΗΣ</a>
                            </li>
                            <li>
                                <a href="">ΚΟΣΤΟΣ ΛΕΙΤΟΥΡΓΙΑΣ</a>
                            </li>
                            <li>
                                <a href="">ΝΕΚΡΟ ΣΗΜΕΙΟ</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a href="">ΧΡΟΝΟΔΙΑΓΡΑΜΜΑ</a>
                    </li>
                    <li>
                        <a href="">ΠΑΡΑΡΤΗΜΑ</a>
                    </li>
                    <li>
                        <a href="">ΣΥΝΟΨΗ</a>
                    </li> -->

                </ul>
            </div>
        </nav>

        <main>
            <router-view/>
        </main>
    </div>

    <footer class="foot">
        <button class="foot__back">ΠΙΣΩ</button>
        <span class="foot__pagination">
            <p>1/2</p>
        </span>
        <button class="foot__next">ΜΠΡΟΣΤΑ</button>
    </footer>
    
  </div>
</template>

<script>

import pdfMake from "pdfmake/build/pdfmake"
import pdfFonts from "pdfmake/build/vfs_fonts"
pdfMake.vfs = pdfFonts.pdfMake.vfs

export default {
 	name: 'Skeleton',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
  	// This function returns a parsed date from the db form(YYYYMMDD) into proper form with slashes(DD/MM/YYYY)
  	dateParser(date){
  		return String(date).slice(6) + "/" 
	 		+ String(date).slice(4, 6) + "/"
	 		+ String(date).slice(0, 4)
  	},
  	// Functions for dynamic PDFMake content generation based on the json
	clientsFun(db) { 
		var clientsArray = [] 			// Array to store the PDFMake content
		var clientsObj = db["clients"]	// Store the object in a local variable

		// Loop through the managers object and format the content in PDFMake form
		for (var i = 0; i < clientsObj.length; i++){
			clientsArray.push([{text: "ID: " 			+ clientsObj[i].ID},
							   {text: "Όνοματεπώνυμο: " + clientsObj[i].Name}])
		}
		return clientsArray
        },
        sevenOneStartFun(db) { 
		var strategyArray = [] 			// Array to store the PDFMake content
		var strategyObj = db["strategy"]	// Store the object in a local variable

		// Loop through the managers object and format the content in PDFMake form
		for (var i = 0; i < strategyObj.length; i++){
			strategyArray.push([{text: "ID επιχειρησιακού σχεδίου: " 			+ strategyObj[i].BusinessPlanId},
							   {text: "Προβολή: " 			+ strategyObj[i].Promotion},
							   {text: "Συνεισφορά: " 			+ strategyObj[i].Contribution},
							   {text: "Είσοδος αγοράς: " 			+ strategyObj[i].MarketEntry},
							   {text: "Δημόσιες σχέσεις: " 			+ strategyObj[i].PublicRelations},
							   {text: "Αποφυγή: " + strategyObj[i].Avoid}])
		}
		return strategyArray
        },
        sevenTwoStartFun(db) { 
		var marketingActionsArray = [] 			// Array to store the PDFMake content
		var marketingActionsObj = db["marketingActions"]	// Store the object in a local variable

		// Loop through the managers object and format the content in PDFMake form
		for (var i = 0; i < marketingActionsObj.length; i++){
			marketingActionsArray.push([{text: "ID: " 			+ marketingActionsObj[i].ID},
							   {text: "ID επιχειρησιακού σχεδίου: " 			+ marketingActionsObj[i].BusinessPlanId},
							   {text: "Τίτλος: " 			+ marketingActionsObj[i].Title},
							   {text: "Χρόνος εκτέλεσης: " 			+ marketingActionsObj[i].ImplementationTime},
							   {text: "Συχνότητα: " 			+ marketingActionsObj[i].Frequency},
							   {text: "Κόστος εκτέλεσης: " 			+ marketingActionsObj[i].ImplementationCost},
							   {text: "Συνολικό κόστος: " + marketingActionsObj[i].TotalCost}])
		}
		return marketingActionsArray
         },
         eightOneStartFun(db) { 
		var startActionsArray = [] 			// Array to store the PDFMake content
		var startActionsObj = db["startActions"]	// Store the object in a local variable

		// Loop through the managers object and format the content in PDFMake form
		for (var i = 0; i < startActionsObj.length; i++){
			startActionsArray.push([{text: "ID: " 			+ startActionsObj[i].ID},
							   {text: "ID επιχειρησιακού σχεδίου: " 			+ startActionsObj[i].BusinessPlanId},
							   {text: "Όνομα: " 			+ startActionsObj[i].Name},
							   {text: "Κόστος δράσης: " + startActionsObj[i].ActionCost}])
		}
		return startActionsArray
         },
         eightTwoStartFun(db) { 
		var functionCostArray = [] 			// Array to store the PDFMake content
		var functionCostObj = db["functionCost"]	// Store the object in a local variable

		// Loop through the managers object and format the content in PDFMake form
		for (var i = 0; i < functionCostObj.length; i++){
			functionCostArray.push([{text: "ID: " 			+ functionCostObj[i].ID},
							   {text: "ID επιχειρησιακού σχεδίου: " 			+ functionCostObj[i].BusinessPlanId},
							   {text: "Όνομα: " 			+ functionCostObj[i].Name},
							   {text: "Κόστος λειτουργίας: " + functionCostObj[i].FunctionCost}])
		}
		return functionCostArray
         },
         eightThreeStartFun(db) { 
		var deadspotsArray = [] 			// Array to store the PDFMake content
		var deadspotsObj = db["deadspots"]	// Store the object in a local variable

		// Loop through the managers object and format the content in PDFMake form
		for (var i = 0; i < deadspotsObj.length; i++){
			deadspotsArray.push([{text: "ID προϊόντος: " 			+ deadspotsObj[i].ProductID},
							   {text: "ID επιχειρησιακού σχεδίου: " 			+ deadspotsObj[i].BusinessPlanId},
							   {text: "Σημείο: " + deadspotsObj[i].Spot}])
		}
		return deadspotsArray
         },
         nineStartFun(db) { 
		var linksArray = [] 			// Array to store the PDFMake content
		var linksObj = db["links"]	// Store the object in a local variable

		// Loop through the managers object and format the content in PDFMake form
		for (var i = 0; i < linksObj.length; i++){
			linksArray.push([{text: "ID: " 			+ linksObj[i].ID},
							   {text: "ID επιχειρησιακού σχεδίου: " 			+ linksObj[i].BusinessPlanId},
							   {text: "URL: " 			+ linksObj[i].URL},
							   {text: "Τίτλος: " 			+ linksObj[i].Title},
							   {text: "Τομέας: " + linksObj[i].Section}])
		}
		return linksArray
         },
         tenStartFun(db) { 
		var conclusionArray = [] 			// Array to store the PDFMake content
		var conclusionObj = db["conclusion"]	// Store the object in a local variable

		// Loop through the managers object and format the content in PDFMake form
		for (var i = 0; i < conclusionObj.length; i++){
			conclusionArray.push([{text: "ID επιχειρησιακού σχεδίου: " 			+ conclusionObj[i].BussinesPlanId},
							   {text: "Κείμενο: " + conclusionObj[i].Text}])
		}
		return conclusionArray
	 },
    exportFunction(){
    	var db = this.$store.state
		// PDFMake code here
		var docDefinition = {
			// Content of the pdf document
			content: [
				// Section 1
				{text: "Επιχειρηματικό Μοντέλο", style: "sectionHeader"},
				" ",
				// Subsection 1.1
				// This content element is a complicated one, with extra "tags" like bold, underline, etc., all contained into the style. 
				// Notice it is inside curly brackets.
				{text: "1.1 Ταυτότητα Επιχείρησης:", style: "subSectionHeader"},
				" ", // Newline
				// This content element is a simple string element, no need for curly brackets, just comma after it.
				"Όνομα επιχείρησης: " 	   + db["identity"][0].Name,
				"Ημερομηνία δημιουργίας: " + this.dateParser(db["identity"][0].Date),
				"Νομική μορφή: " 		   + db["identity"][0].LegalForm,
				"Τύπος επιχείρησης: "      + db["identity"][0].OrderOfBusiness,
				" ",
				"Πελάτες: ",
				// Due to the "ol" tag, it needs curly brackets. Equivalent to {ol: [firstItem, secondItem]} syntax.
				{ol: this.clientsFun(db)},

                                // Section 7
				{text: "Χρηματοοικονομικός Σχεδιασμός", style: "sectionHeader"},
				" ",
				// Subsection 7.1
				// This content element is a complicated one, with extra "tags" like bold, underline, etc., all contained into the style. 
				// Notice it is inside curly brackets.
				{text: "7.1 Στρατηγική:", style: "subSectionHeader"},
				" ", // Newline
				// Due to the "ol" tag, it needs curly brackets. Equivalent to {ol: [firstItem, secondItem]} syntax.
				{ol: this.sevenOneStartFun(db)},
                                " ",
                                // Subsection 7.2
				// This content element is a complicated one, with extra "tags" like bold, underline, etc., all contained into the style. 
				// Notice it is inside curly brackets.
				{text: "7.2 Ενέργειες marketing:", style: "subSectionHeader"},
				" ", // Newline
				// Due to the "ol" tag, it needs curly brackets. Equivalent to {ol: [firstItem, secondItem]} syntax.
				{ol: this.sevenTwoStartFun(db)},
                                " ",
                                // Section 8
				{text: "Χρονοδιάγραμμα", style: "sectionHeader"},
				" ",
				// Subsection 8.1
				// This content element is a complicated one, with extra "tags" like bold, underline, etc., all contained into the style. 
				// Notice it is inside curly brackets.
				{text: "8.1 Ενέργειες εκκίνησης:", style: "subSectionHeader"},
				" ", // Newline
				// Due to the "ol" tag, it needs curly brackets. Equivalent to {ol: [firstItem, secondItem]} syntax.
				{ol: this.eightOneStartFun(db)},
                                " ",
                                // Subsection 8.2
				// This content element is a complicated one, with extra "tags" like bold, underline, etc., all contained into the style. 
				// Notice it is inside curly brackets.
				{text: "8.2 Κόστος λειτουργίας:", style: "subSectionHeader"},
				" ", // Newline
				// Due to the "ol" tag, it needs curly brackets. Equivalent to {ol: [firstItem, secondItem]} syntax.
				{ol: this.eightTwoStartFun(db)},
                                {text: "Συνολικό κόστος λειτουργίας: " + String(db.functionCost.FunctionsTotalCost) + "€", bold: true},
                                " ",
                                // Subsection 8.3
				// This content element is a complicated one, with extra "tags" like bold, underline, etc., all contained into the style. 
				// Notice it is inside curly brackets.
				{text: "8.3 Νεκρά σημεία:", style: "subSectionHeader"},
				" ", // Newline
				// Due to the "ol" tag, it needs curly brackets. Equivalent to {ol: [firstItem, secondItem]} syntax.
				{ol: this.eightThreeStartFun(db)},
                                " ",
                                // Section 9
				{text: "Παράρτημα", style: "sectionHeader"},
				" ",
				// Due to the "ol" tag, it needs curly brackets. Equivalent to {ol: [firstItem, secondItem]} syntax.
				{ol: this.nineStartFun(db)},
                                " ",
                                // Section 10
				{text: "Σύνοψη", style: "sectionHeader"},
				" ",
				// Due to the "ol" tag, it needs curly brackets. Equivalent to {ol: [firstItem, secondItem]} syntax.
				{ol: this.tenStartFun(db)},
                                " "," ",

			], // Content array end

			styles: {
			    sectionHeader: {
			      bold: true, underline: true, fontSize: 20, alignment: "left", decoration:"underline"
			    },
			    subSectionHeader: {
			      bold: true, underline: true, fontSize: 15, alignment: "left", decoration:"underline"
			    }
			  }

		} // docDefinition end
			
		// Download the PDF, named after the business name given in section 1.1
		pdfMake.createPdf(docDefinition).download(db["identity"][0].Name + "BusinessPlan.pdf");
    } // ExportFun end		
  }
}
</script>

<style>
        /* APP */

        .skeleton {
            display: flex;
            flex-direction: column;
            justify-content: initial;
            align-items: stretch;
            min-height: 100vh;
        }


        /* HEADER */

        .head {
            background-color: rgb(30, 33, 51);
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 80px;
            ;
        }

        .head__logo {
            margin-left: 20px;
        }

        .head__export {
            color: #fff;
            display: flex;
            margin-right: 100px;
            align-items: center;
        }


        .head__avatar {
            height: 70px;
            width: 70px;
            border-radius: 50%;
            margin-right: 20px;
        }

        .head__export p {
            margin-left: 5px;
            font-size: 20px;
        }

        .head__export i {}


        /* FOOTER */

        footer {
            background-color: rgb(203, 202, 202);
            height: 60px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .foot__back {
            margin-right: 30px;
            background-color: rgb(41, 152, 88);
            color: white;
            width: 100px;
            height: 40px;
            display: flex;
            justify-content: center;
            align-items: center;
            border-style: none;
        }

        .foot__next {
            margin-left: 30px;
            background-color: rgb(41, 152, 88);
            color: white;
            width: 100px;
            height: 40px;
            display: flex;
            justify-content: center;
            align-items: center;
            border-style: none;
        }

        .foot__pagination {
            font-size: 20px;
            font-weight: 600;
            color: black;
        }


        main {
            flex-grow: 1;
        }

        .main_container {
            flex-grow: 1;
            display: flex;
            justify-content: space-between;
            align-items: stretch;
        }

        nav {
            background-color: rgb(30, 33, 51);
            width: 350px;
        }


        /* SECTIONS MENU */

        .sections-menu {}

        .sections-menu ul {
            list-style: none;
            margin: 0;
        }

        .sections-menu ul li {
            padding: 15px;
            position: relative;
            width: 350px;
            border-top: 1px solid black;
            background-color: rgb(30, 33, 51);
        }

        .sections-menu ul li {
            border-right: 5px solid rgb(61, 65, 90);
        }

        .sections-menu ul ul {
            opacity: 0;
            position: absolute;
            visibility: hidden;
            left: 100%;
            top: -2%;
            background-color: rgb(40, 44, 63);
        }

        .sections-menu ul ul li {
            background-color: rgb(79, 84, 115);
            width: 250px;
        }

        .sections-menu ul li:hover ul {
            opacity: 1;
            visibility: visible;
        }

        .sections-menu ul li a {
            color: white;
        }


        /* BASIC ELEMENTS */

        .basic_button {
            background-color: rgb(24, 146, 105);
            width: 100px;
            height: 40px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
    </style>
