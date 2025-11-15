# missingSMILES.rq
**Code examples:** [curl](#curl)
### SPARQL
```sparql
PREFIX dbpedia2: <http://dbpedia.org/property/>

SELECT ?s ?article ?item ?itemLabel WITH {
  SELECT DISTINCT ?s ?article WHERE {
    SERVICE <https://dbpedia.org/sparql> {
      ?s dbpedia2:wikiPageUsesTemplate <http://dbpedia.org/resource/Template:Chembox>.
      ?article_db foaf:primaryTopic ?s.
    }
    BIND (IRI(REPLACE(STR(?article_db), "http://", "https://", "i")) AS ?article)
  }
} AS %DBPEDIA WITH {
  SELECT DISTINCT ?s ?article ?item WHERE {
    INCLUDE %DBPEDIA
    ?article schema:about ?item .
    MINUS { ?item wdt:P233 [] }
    MINUS { ?item wdt:P2017 [] }
    MINUS { ?item wdt:P10718 [] }
  }
} AS %CHEMICALS WHERE {
  INCLUDE %CHEMICALS
  VALUES ?chemicals { wd:Q113145171 wd:Q59199015 }
  ?item wdt:P31 ?chemicals.
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}
ORDER BY ASC(?item)
```
[Execute](https://query.wikidata.org/embed.html#PREFIX%20dbpedia2%3A%20%3Chttp%3A%2F%2Fdbpedia.org%2Fproperty%2F%3E%0A%0ASELECT%20%3Fs%20%3Farticle%20%3Fitem%20%3FitemLabel%20WITH%20%7B%0A%20%20SELECT%20DISTINCT%20%3Fs%20%3Farticle%20WHERE%20%7B%0A%20%20%20%20SERVICE%20%3Chttps%3A%2F%2Fdbpedia.org%2Fsparql%3E%20%7B%0A%20%20%20%20%20%20%3Fs%20dbpedia2%3AwikiPageUsesTemplate%20%3Chttp%3A%2F%2Fdbpedia.org%2Fresource%2FTemplate%3AChembox%3E.%0A%20%20%20%20%20%20%3Farticle_db%20foaf%3AprimaryTopic%20%3Fs.%0A%20%20%20%20%7D%0A%20%20%20%20BIND%20%28IRI%28REPLACE%28STR%28%3Farticle_db%29%2C%20%22http%3A%2F%2F%22%2C%20%22https%3A%2F%2F%22%2C%20%22i%22%29%29%20AS%20%3Farticle%29%0A%20%20%7D%0A%7D%20AS%20%25DBPEDIA%20WITH%20%7B%0A%20%20SELECT%20DISTINCT%20%3Fs%20%3Farticle%20%3Fitem%20WHERE%20%7B%0A%20%20%20%20INCLUDE%20%25DBPEDIA%0A%20%20%20%20%3Farticle%20schema%3Aabout%20%3Fitem%20.%0A%20%20%20%20MINUS%20%7B%20%3Fitem%20wdt%3AP233%20%5B%5D%20%7D%0A%20%20%20%20MINUS%20%7B%20%3Fitem%20wdt%3AP2017%20%5B%5D%20%7D%0A%20%20%20%20MINUS%20%7B%20%3Fitem%20wdt%3AP10718%20%5B%5D%20%7D%0A%20%20%7D%0A%7D%20AS%20%25CHEMICALS%20WHERE%20%7B%0A%20%20INCLUDE%20%25CHEMICALS%0A%20%20VALUES%20%3Fchemicals%20%7B%20wd%3AQ113145171%20wd%3AQ59199015%20%7D%0A%20%20%3Fitem%20wdt%3AP31%20%3Fchemicals.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D%0AORDER%20BY%20ASC%28%3Fitem%29%0A) or [Edit](https://query.wikidata.org/#PREFIX%20dbpedia2%3A%20%3Chttp%3A%2F%2Fdbpedia.org%2Fproperty%2F%3E%0A%0ASELECT%20%3Fs%20%3Farticle%20%3Fitem%20%3FitemLabel%20WITH%20%7B%0A%20%20SELECT%20DISTINCT%20%3Fs%20%3Farticle%20WHERE%20%7B%0A%20%20%20%20SERVICE%20%3Chttps%3A%2F%2Fdbpedia.org%2Fsparql%3E%20%7B%0A%20%20%20%20%20%20%3Fs%20dbpedia2%3AwikiPageUsesTemplate%20%3Chttp%3A%2F%2Fdbpedia.org%2Fresource%2FTemplate%3AChembox%3E.%0A%20%20%20%20%20%20%3Farticle_db%20foaf%3AprimaryTopic%20%3Fs.%0A%20%20%20%20%7D%0A%20%20%20%20BIND%20%28IRI%28REPLACE%28STR%28%3Farticle_db%29%2C%20%22http%3A%2F%2F%22%2C%20%22https%3A%2F%2F%22%2C%20%22i%22%29%29%20AS%20%3Farticle%29%0A%20%20%7D%0A%7D%20AS%20%25DBPEDIA%20WITH%20%7B%0A%20%20SELECT%20DISTINCT%20%3Fs%20%3Farticle%20%3Fitem%20WHERE%20%7B%0A%20%20%20%20INCLUDE%20%25DBPEDIA%0A%20%20%20%20%3Farticle%20schema%3Aabout%20%3Fitem%20.%0A%20%20%20%20MINUS%20%7B%20%3Fitem%20wdt%3AP233%20%5B%5D%20%7D%0A%20%20%20%20MINUS%20%7B%20%3Fitem%20wdt%3AP2017%20%5B%5D%20%7D%0A%20%20%20%20MINUS%20%7B%20%3Fitem%20wdt%3AP10718%20%5B%5D%20%7D%0A%20%20%7D%0A%7D%20AS%20%25CHEMICALS%20WHERE%20%7B%0A%20%20INCLUDE%20%25CHEMICALS%0A%20%20VALUES%20%3Fchemicals%20%7B%20wd%3AQ113145171%20wd%3AQ59199015%20%7D%0A%20%20%3Fitem%20wdt%3AP31%20%3Fchemicals.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D%0AORDER%20BY%20ASC%28%3Fitem%29%0A)


### Output
<table>
  <tr>
    <td><b>s</b></td>
    <td><b>article</b></td>
    <td><b>item</b></td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Vanadium(V)_chloride_chlorimide</td>
    <td>https://en.wikipedia.org/wiki/Vanadium(V)_chloride_chlorimide</td>
    <td><a href="https://scholia.toolforge.org/Q100341984">vanadium(V) chloride chlorimide</a> (<a href="http://www.wikidata.org/entity/Q100341984">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Potassium_tetracarbonyliron_hydride</td>
    <td>https://en.wikipedia.org/wiki/Potassium_tetracarbonyliron_hydride</td>
    <td><a href="https://scholia.toolforge.org/Q100552750">potassium tetracarbonyliron hydride</a> (<a href="http://www.wikidata.org/entity/Q100552750">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/(Triphenylphosphine)iron_tetracarbonyl</td>
    <td>https://en.wikipedia.org/wiki/(Triphenylphosphine)iron_tetracarbonyl</td>
    <td><a href="https://scholia.toolforge.org/Q100693702">(triphenylphosphine)iron tetracarbonyl</a> (<a href="http://www.wikidata.org/entity/Q100693702">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Bis(triphenylphosphine)iron_tricarbonyl</td>
    <td>https://en.wikipedia.org/wiki/Bis(triphenylphosphine)iron_tricarbonyl</td>
    <td><a href="https://scholia.toolforge.org/Q100693878">bis(triphenylphosphine)iron tricarbonyl</a> (<a href="http://www.wikidata.org/entity/Q100693878">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Zinc_diphosphide</td>
    <td>https://en.wikipedia.org/wiki/Zinc_diphosphide</td>
    <td><a href="https://scholia.toolforge.org/Q100775201">zinc diphosphide</a> (<a href="http://www.wikidata.org/entity/Q100775201">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Caesium_superoxide</td>
    <td>https://en.wikipedia.org/wiki/Caesium_superoxide</td>
    <td><a href="https://scholia.toolforge.org/Q1025477">caesium superoxide</a> (<a href="http://www.wikidata.org/entity/Q1025477">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Caesium_ozonide</td>
    <td>https://en.wikipedia.org/wiki/Caesium_ozonide</td>
    <td><a href="https://scholia.toolforge.org/Q1025482">cesium ozonide</a> (<a href="http://www.wikidata.org/entity/Q1025482">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Californium(II)_iodide</td>
    <td>https://en.wikipedia.org/wiki/Californium(II)_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q1026963">californium(II) iodide</a> (<a href="http://www.wikidata.org/entity/Q1026963">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Californium(III)_chloride</td>
    <td>https://en.wikipedia.org/wiki/Californium(III)_chloride</td>
    <td><a href="https://scholia.toolforge.org/Q1026968">californium(III) chloride</a> (<a href="http://www.wikidata.org/entity/Q1026968">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Californium(III)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Californium(III)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q1026969">californium(III) fluoride</a> (<a href="http://www.wikidata.org/entity/Q1026969">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Californium(III)_iodide</td>
    <td>https://en.wikipedia.org/wiki/Californium(III)_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q1026970">californium(III) iodide</a> (<a href="http://www.wikidata.org/entity/Q1026970">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Californium(III)_oxide</td>
    <td>https://en.wikipedia.org/wiki/Californium(III)_oxide</td>
    <td><a href="https://scholia.toolforge.org/Q1026974">californium(III) oxide</a> (<a href="http://www.wikidata.org/entity/Q1026974">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Californium_tetrafluoride</td>
    <td>https://en.wikipedia.org/wiki/Californium_tetrafluoride</td>
    <td><a href="https://scholia.toolforge.org/Q1026975">californium(IV) fluoride</a> (<a href="http://www.wikidata.org/entity/Q1026975">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Californium(III)_oxyfluoride</td>
    <td>https://en.wikipedia.org/wiki/Californium(III)_oxyfluoride</td>
    <td><a href="https://scholia.toolforge.org/Q1026977">californium(III) oxyfluoride</a> (<a href="http://www.wikidata.org/entity/Q1026977">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Californium(IV)_oxide</td>
    <td>https://en.wikipedia.org/wiki/Californium(IV)_oxide</td>
    <td><a href="https://scholia.toolforge.org/Q1026979">californium(IV) oxide</a> (<a href="http://www.wikidata.org/entity/Q1026979">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Potassium_nonahydridorhenate</td>
    <td>https://en.wikipedia.org/wiki/Potassium_nonahydridorhenate</td>
    <td><a href="https://scholia.toolforge.org/Q1089194">potassium nonahydridorhenate</a> (<a href="http://www.wikidata.org/entity/Q1089194">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Xenon_dioxide</td>
    <td>https://en.wikipedia.org/wiki/Xenon_dioxide</td>
    <td><a href="https://scholia.toolforge.org/Q1089242">xenon dioxide</a> (<a href="http://www.wikidata.org/entity/Q1089242">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Lithium_imide</td>
    <td>https://en.wikipedia.org/wiki/Lithium_imide</td>
    <td><a href="https://scholia.toolforge.org/Q1090011">lithium imide</a> (<a href="http://www.wikidata.org/entity/Q1090011">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Strontium_nitride</td>
    <td>https://en.wikipedia.org/wiki/Strontium_nitride</td>
    <td><a href="https://scholia.toolforge.org/Q1091256">strontium nitride</a> (<a href="http://www.wikidata.org/entity/Q1091256">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Calcium(I)_chloride</td>
    <td>https://en.wikipedia.org/wiki/Calcium(I)_chloride</td>
    <td><a href="https://scholia.toolforge.org/Q1096750">calcium(I) chloride</a> (<a href="http://www.wikidata.org/entity/Q1096750">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Lanthanum_cuprate</td>
    <td>https://en.wikipedia.org/wiki/Lanthanum_cuprate</td>
    <td><a href="https://scholia.toolforge.org/Q111012543">lanthanum cuprate</a> (<a href="http://www.wikidata.org/entity/Q111012543">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Hopeanol</td>
    <td>https://en.wikipedia.org/wiki/Hopeanol</td>
    <td><a href="https://scholia.toolforge.org/Q111165883">Hopeanol</a> (<a href="http://www.wikidata.org/entity/Q111165883">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Caesium_tribromide</td>
    <td>https://en.wikipedia.org/wiki/Caesium_tribromide</td>
    <td><a href="https://scholia.toolforge.org/Q113826923">Caesium tribromide</a> (<a href="http://www.wikidata.org/entity/Q113826923">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Curium(III)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Curium(III)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q1144604">curium(III) fluoride</a> (<a href="http://www.wikidata.org/entity/Q1144604">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Curium(III)_chloride</td>
    <td>https://en.wikipedia.org/wiki/Curium(III)_chloride</td>
    <td><a href="https://scholia.toolforge.org/Q1144605">curium(III) chloride</a> (<a href="http://www.wikidata.org/entity/Q1144605">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Curium(III)_iodide</td>
    <td>https://en.wikipedia.org/wiki/Curium(III)_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q1144608">curium(III) iodide</a> (<a href="http://www.wikidata.org/entity/Q1144608">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Curium(IV)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Curium(IV)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q1144613">curium(IV) fluoride</a> (<a href="http://www.wikidata.org/entity/Q1144613">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cobalt(II)_azide</td>
    <td>https://en.wikipedia.org/wiki/Cobalt(II)_azide</td>
    <td><a href="https://scholia.toolforge.org/Q114836185">Cobalt(II) azide</a> (<a href="http://www.wikidata.org/entity/Q114836185">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Nickel_azide</td>
    <td>https://en.wikipedia.org/wiki/Nickel_azide</td>
    <td><a href="https://scholia.toolforge.org/Q114836251">Nickel azide</a> (<a href="http://www.wikidata.org/entity/Q114836251">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Oxygen_monofluoride</td>
    <td>https://en.wikipedia.org/wiki/Oxygen_monofluoride</td>
    <td><a href="https://scholia.toolforge.org/Q117314466">oxygen monofluoride</a> (<a href="http://www.wikidata.org/entity/Q117314466">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Gold(III)_phosphate</td>
    <td>https://en.wikipedia.org/wiki/Gold(III)_phosphate</td>
    <td><a href="https://scholia.toolforge.org/Q117354168">gold(III) phosphate</a> (<a href="http://www.wikidata.org/entity/Q117354168">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Neodymium(II)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Neodymium(II)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q123982358">neodymium difluoride</a> (<a href="http://www.wikidata.org/entity/Q123982358">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Sorbitan_monopalmitate</td>
    <td>https://en.wikipedia.org/wiki/Sorbitan_monopalmitate</td>
    <td><a href="https://scholia.toolforge.org/Q1300070">sorbitan monopalmitate</a> (<a href="http://www.wikidata.org/entity/Q1300070">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Potassium_polonide</td>
    <td>https://en.wikipedia.org/wiki/Potassium_polonide</td>
    <td><a href="https://scholia.toolforge.org/Q13518697">potassium polonide</a> (<a href="http://www.wikidata.org/entity/Q13518697">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Potassium_chlorochromate</td>
    <td>https://en.wikipedia.org/wiki/Potassium_chlorochromate</td>
    <td><a href="https://scholia.toolforge.org/Q13582207">potassium chlorochromate</a> (<a href="http://www.wikidata.org/entity/Q13582207">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Diamphotoxin</td>
    <td>https://en.wikipedia.org/wiki/Diamphotoxin</td>
    <td><a href="https://scholia.toolforge.org/Q14305118">diamphotoxin</a> (<a href="http://www.wikidata.org/entity/Q14305118">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Promethium(III)_iodide</td>
    <td>https://en.wikipedia.org/wiki/Promethium(III)_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q1473876">promethium(III) iodide</a> (<a href="http://www.wikidata.org/entity/Q1473876">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Copper_indium_gallium_selenide</td>
    <td>https://en.wikipedia.org/wiki/Copper_indium_gallium_selenide</td>
    <td><a href="https://scholia.toolforge.org/Q15023366">Copper indium gallium selenide</a> (<a href="http://www.wikidata.org/entity/Q15023366">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dibromine_monoxide</td>
    <td>https://en.wikipedia.org/wiki/Dibromine_monoxide</td>
    <td><a href="https://scholia.toolforge.org/Q15142952">dibromine monoxide</a> (<a href="http://www.wikidata.org/entity/Q15142952">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Promethium(III)_bromide</td>
    <td>https://en.wikipedia.org/wiki/Promethium(III)_bromide</td>
    <td><a href="https://scholia.toolforge.org/Q1547180">promethium(III) bromide</a> (<a href="http://www.wikidata.org/entity/Q1547180">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Manganese(II)_perchlorate</td>
    <td>https://en.wikipedia.org/wiki/Manganese(II)_perchlorate</td>
    <td><a href="https://scholia.toolforge.org/Q15627466">manganese(II) perchlorate</a> (<a href="http://www.wikidata.org/entity/Q15627466">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ytterbium(II)_hydride</td>
    <td>https://en.wikipedia.org/wiki/Ytterbium(II)_hydride</td>
    <td><a href="https://scholia.toolforge.org/Q15628015">ytterbium(II) hydride</a> (<a href="http://www.wikidata.org/entity/Q15628015">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ytterbium(II)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Ytterbium(II)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q15628023">ytterbium(II) fluoride</a> (<a href="http://www.wikidata.org/entity/Q15628023">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Iridium_trifluoride</td>
    <td>https://en.wikipedia.org/wiki/Iridium_trifluoride</td>
    <td><a href="https://scholia.toolforge.org/Q15628046">iridium trifluoride</a> (<a href="http://www.wikidata.org/entity/Q15628046">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Periodyl_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Periodyl_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q15628057">periodyl fluoride</a> (<a href="http://www.wikidata.org/entity/Q15628057">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Iodine_trifluoride_dioxide</td>
    <td>https://en.wikipedia.org/wiki/Iodine_trifluoride_dioxide</td>
    <td><a href="https://scholia.toolforge.org/Q15628058">iodine trifluoride dioxide</a> (<a href="http://www.wikidata.org/entity/Q15628058">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Iodosyl_trifluoride</td>
    <td>https://en.wikipedia.org/wiki/Iodosyl_trifluoride</td>
    <td><a href="https://scholia.toolforge.org/Q15628060">iodine trifluoride oxide</a> (<a href="http://www.wikidata.org/entity/Q15628060">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Diiodosyl_sulfate</td>
    <td>https://en.wikipedia.org/wiki/Diiodosyl_sulfate</td>
    <td><a href="https://scholia.toolforge.org/Q15628063">iodosyl sulfate</a> (<a href="http://www.wikidata.org/entity/Q15628063">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ammonium_hexafluoroindate</td>
    <td>https://en.wikipedia.org/wiki/Ammonium_hexafluoroindate</td>
    <td><a href="https://scholia.toolforge.org/Q15628084">Ammonium hexafluoroindate</a> (<a href="http://www.wikidata.org/entity/Q15628084">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Diiron_silicide</td>
    <td>https://en.wikipedia.org/wiki/Diiron_silicide</td>
    <td><a href="https://scholia.toolforge.org/Q15628164">Diiron silicide</a> (<a href="http://www.wikidata.org/entity/Q15628164">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Potassium_dithioferrate</td>
    <td>https://en.wikipedia.org/wiki/Potassium_dithioferrate</td>
    <td><a href="https://scholia.toolforge.org/Q15628174">potassium dithioferrate</a> (<a href="http://www.wikidata.org/entity/Q15628174">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Holmium_nitride</td>
    <td>https://en.wikipedia.org/wiki/Holmium_nitride</td>
    <td><a href="https://scholia.toolforge.org/Q15628259">holmium nitride</a> (<a href="http://www.wikidata.org/entity/Q15628259">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Hafnium(III)_iodide</td>
    <td>https://en.wikipedia.org/wiki/Hafnium(III)_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q15628318">hafnium(III) iodide</a> (<a href="http://www.wikidata.org/entity/Q15628318">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Bromosyl_trifluoride</td>
    <td>https://en.wikipedia.org/wiki/Bromosyl_trifluoride</td>
    <td><a href="https://scholia.toolforge.org/Q15628395">Bromosyl trifluoride</a> (<a href="http://www.wikidata.org/entity/Q15628395">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Hexaborane(12)</td>
    <td>https://en.wikipedia.org/wiki/Hexaborane(12)</td>
    <td><a href="https://scholia.toolforge.org/Q15628412">hexaborane(12)</a> (<a href="http://www.wikidata.org/entity/Q15628412">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Actinium_oxyfluoride</td>
    <td>https://en.wikipedia.org/wiki/Actinium_oxyfluoride</td>
    <td><a href="https://scholia.toolforge.org/Q15628467">actinium oxyfluoride</a> (<a href="http://www.wikidata.org/entity/Q15628467">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Osmium_pentafluoride</td>
    <td>https://en.wikipedia.org/wiki/Osmium_pentafluoride</td>
    <td><a href="https://scholia.toolforge.org/Q15632747">osmium(V) fluoride</a> (<a href="http://www.wikidata.org/entity/Q15632747">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Samarium(II)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Samarium(II)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q15632780">samarium(II) fluoride</a> (<a href="http://www.wikidata.org/entity/Q15632780">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Tantalum(IV)_iodide</td>
    <td>https://en.wikipedia.org/wiki/Tantalum(IV)_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q15632854">tantalum iodide</a> (<a href="http://www.wikidata.org/entity/Q15632854">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Curium_oxalate</td>
    <td>https://en.wikipedia.org/wiki/Curium_oxalate</td>
    <td><a href="https://scholia.toolforge.org/Q15632865">curium(III) oxalate</a> (<a href="http://www.wikidata.org/entity/Q15632865">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Agatolimod</td>
    <td>https://en.wikipedia.org/wiki/Agatolimod</td>
    <td><a href="https://scholia.toolforge.org/Q15633941">agatolimod</a> (<a href="http://www.wikidata.org/entity/Q15633941">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Aganirsen</td>
    <td>https://en.wikipedia.org/wiki/Aganirsen</td>
    <td><a href="https://scholia.toolforge.org/Q15633943">aganirsen</a> (<a href="http://www.wikidata.org/entity/Q15633943">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Diiron_propanedithiolate_hexacarbonyl</td>
    <td>https://en.wikipedia.org/wiki/Diiron_propanedithiolate_hexacarbonyl</td>
    <td><a href="https://scholia.toolforge.org/Q15634097">Diiron propanedithiolate hexacarbonyl</a> (<a href="http://www.wikidata.org/entity/Q15634097">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dichlorobis(triphenylphosphine)nickel(II)</td>
    <td>https://en.wikipedia.org/wiki/Dichlorobis(triphenylphosphine)nickel(II)</td>
    <td><a href="https://scholia.toolforge.org/Q15634098">bis(triphenylphosphine)nickel chloride</a> (<a href="http://www.wikidata.org/entity/Q15634098">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Chlorobis(dppe)iron_hydride</td>
    <td>https://en.wikipedia.org/wiki/Chlorobis(dppe)iron_hydride</td>
    <td><a href="https://scholia.toolforge.org/Q15634153">Chlorohydridobis(bis-1,2-(diphenylphosphino)ethane)iron(II)</a> (<a href="http://www.wikidata.org/entity/Q15634153">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Trimethylsilyl_cyclopentadiene</td>
    <td>https://en.wikipedia.org/wiki/Trimethylsilyl_cyclopentadiene</td>
    <td><a href="https://scholia.toolforge.org/Q15634158">Trimethylsilyl cyclopentadiene</a> (<a href="http://www.wikidata.org/entity/Q15634158">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Bis(dinitrogen)bis(1,2-bis(diphenylphosphino)ethane)molybdenum(0)</td>
    <td>https://en.wikipedia.org/wiki/Bis(dinitrogen)bis(1,2-bis(diphenylphosphino)ethane)molybdenum(0)</td>
    <td><a href="https://scholia.toolforge.org/Q15634210">Bis(dinitrogen)bis(1,2-bis(diphenylphosphino)ethane)molybdenum(0)</a> (<a href="http://www.wikidata.org/entity/Q15634210">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/3,5-Dimethylpiperidine</td>
    <td>https://en.wikipedia.org/wiki/3,5-Dimethylpiperidine</td>
    <td><a href="https://scholia.toolforge.org/Q15634223">3,5-dimethylpiperidine</a> (<a href="http://www.wikidata.org/entity/Q15634223">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Pseudopterosin_E</td>
    <td>https://en.wikipedia.org/wiki/Pseudopterosin_E</td>
    <td><a href="https://scholia.toolforge.org/Q15634229">Pseudopterosin E</a> (<a href="http://www.wikidata.org/entity/Q15634229">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Scholarine</td>
    <td>https://en.wikipedia.org/wiki/N-Formylscholarine</td>
    <td><a href="https://scholia.toolforge.org/Q15634232">N-Formylscholarine</a> (<a href="http://www.wikidata.org/entity/Q15634232">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Mannopeptimycin_glycopeptide</td>
    <td>https://en.wikipedia.org/wiki/Mannopeptimycin_glycopeptide</td>
    <td><a href="https://scholia.toolforge.org/Q15634237">Mannopeptimycin glycopeptide</a> (<a href="http://www.wikidata.org/entity/Q15634237">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Magnesium_iron_hexahydride</td>
    <td>https://en.wikipedia.org/wiki/Magnesium_iron_hexahydride</td>
    <td><a href="https://scholia.toolforge.org/Q15634287">magnesium iron hexahydride</a> (<a href="http://www.wikidata.org/entity/Q15634287">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Prodelphinidin_C2</td>
    <td>https://en.wikipedia.org/wiki/Prodelphinidin_C2</td>
    <td><a href="https://scholia.toolforge.org/Q15634380">Prodelphinidin C2</a> (<a href="http://www.wikidata.org/entity/Q15634380">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Prodelphinidin_B9</td>
    <td>https://en.wikipedia.org/wiki/Prodelphinidin_B9</td>
    <td><a href="https://scholia.toolforge.org/Q15634381">Prodelphinidin B9</a> (<a href="http://www.wikidata.org/entity/Q15634381">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Rubidium_oxalate</td>
    <td>https://en.wikipedia.org/wiki/Rubidium_oxalate</td>
    <td><a href="https://scholia.toolforge.org/Q1616359">rubidium oxalate</a> (<a href="http://www.wikidata.org/entity/Q1616359">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Rubidium_triiodide</td>
    <td>https://en.wikipedia.org/wiki/Rubidium_triiodide</td>
    <td><a href="https://scholia.toolforge.org/Q1651653">rubidium triiodide</a> (<a href="http://www.wikidata.org/entity/Q1651653">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Neopluramycin</td>
    <td>https://en.wikipedia.org/wiki/Neopluramycin</td>
    <td><a href="https://scholia.toolforge.org/Q16889234">neopluramycin</a> (<a href="http://www.wikidata.org/entity/Q16889234">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Bis(triphenylphosphine)platinum_chloride</td>
    <td>https://en.wikipedia.org/wiki/Bis(triphenylphosphine)platinum_chloride</td>
    <td><a href="https://scholia.toolforge.org/Q17005128">bis(triphenylphosphine)platinum chloride</a> (<a href="http://www.wikidata.org/entity/Q17005128">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Thorium_diiodide</td>
    <td>https://en.wikipedia.org/wiki/Thorium_diiodide</td>
    <td><a href="https://scholia.toolforge.org/Q17265575">thorium diiodide</a> (<a href="http://www.wikidata.org/entity/Q17265575">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Protactinium(V)_bromide</td>
    <td>https://en.wikipedia.org/wiki/Protactinium(V)_bromide</td>
    <td><a href="https://scholia.toolforge.org/Q17325761">protactinium(V) bromide</a> (<a href="http://www.wikidata.org/entity/Q17325761">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Protactinium(V)_iodide</td>
    <td>https://en.wikipedia.org/wiki/Protactinium(V)_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q17325762">protactinium(V) iodide</a> (<a href="http://www.wikidata.org/entity/Q17325762">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Neptunium_diarsenide</td>
    <td>https://en.wikipedia.org/wiki/Neptunium_diarsenide</td>
    <td><a href="https://scholia.toolforge.org/Q17749250">neptunium diarsenide</a> (<a href="http://www.wikidata.org/entity/Q17749250">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Copper(II)_acetylacetonate</td>
    <td>https://en.wikipedia.org/wiki/Copper(II)_acetylacetonate</td>
    <td><a href="https://scholia.toolforge.org/Q1792796">copper(II) acetylacetonate</a> (<a href="http://www.wikidata.org/entity/Q1792796">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Promethium(III)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Promethium(III)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q1796798">promethium(III) fluoride</a> (<a href="http://www.wikidata.org/entity/Q1796798">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Lanthanum_manganite</td>
    <td>https://en.wikipedia.org/wiki/Lanthanum_manganite</td>
    <td><a href="https://scholia.toolforge.org/Q18345146">lanthanum manganite</a> (<a href="http://www.wikidata.org/entity/Q18345146">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cyphostemmin_B</td>
    <td>https://en.wikipedia.org/wiki/Cyphostemmin_B</td>
    <td><a href="https://scholia.toolforge.org/Q18349723">cyphostemmin B</a> (<a href="http://www.wikidata.org/entity/Q18349723">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Xenon_nitrate</td>
    <td>https://en.wikipedia.org/wiki/Xenon_nitrate</td>
    <td><a href="https://scholia.toolforge.org/Q18395689">xenon nitrate</a> (<a href="http://www.wikidata.org/entity/Q18395689">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Plutonium(IV)_sulfate</td>
    <td>https://en.wikipedia.org/wiki/Plutonium(IV)_sulfate</td>
    <td><a href="https://scholia.toolforge.org/Q19365941">plutonium(IV) sulfate</a> (<a href="http://www.wikidata.org/entity/Q19365941">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Neptunium(III)_bromide</td>
    <td>https://en.wikipedia.org/wiki/Neptunium(III)_bromide</td>
    <td><a href="https://scholia.toolforge.org/Q1977868">neptunium(III) bromide</a> (<a href="http://www.wikidata.org/entity/Q1977868">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Neptunium(III)_chloride</td>
    <td>https://en.wikipedia.org/wiki/Neptunium(III)_chloride</td>
    <td><a href="https://scholia.toolforge.org/Q1977871">neptunium(III) chloride</a> (<a href="http://www.wikidata.org/entity/Q1977871">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Neptunium(III)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Neptunium(III)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q1977872">neptunium(III) fluoride</a> (<a href="http://www.wikidata.org/entity/Q1977872">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Neptunium(III)_iodide</td>
    <td>https://en.wikipedia.org/wiki/Neptunium(III)_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q1977874">neptunium(III) iodide</a> (<a href="http://www.wikidata.org/entity/Q1977874">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Neptunium_tetrabromide</td>
    <td>https://en.wikipedia.org/wiki/Neptunium_tetrabromide</td>
    <td><a href="https://scholia.toolforge.org/Q1977879">neptunium(IV) bromide</a> (<a href="http://www.wikidata.org/entity/Q1977879">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Neptunium_tetrachloride</td>
    <td>https://en.wikipedia.org/wiki/Neptunium_tetrachloride</td>
    <td><a href="https://scholia.toolforge.org/Q1977880">neptunium(IV) chloride</a> (<a href="http://www.wikidata.org/entity/Q1977880">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Neptunium(IV)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Neptunium(IV)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q1977882">neptunium(IV) fluoride</a> (<a href="http://www.wikidata.org/entity/Q1977882">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Nickel_hydrazine_nitrate</td>
    <td>https://en.wikipedia.org/wiki/Nickel_hydrazine_nitrate</td>
    <td><a href="https://scholia.toolforge.org/Q1985626">nickel hydrazine nitrate</a> (<a href="http://www.wikidata.org/entity/Q1985626">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dicyanamide</td>
    <td>https://en.wikipedia.org/wiki/Dicyanamide</td>
    <td><a href="https://scholia.toolforge.org/Q19885186">dicyanamide</a> (<a href="http://www.wikidata.org/entity/Q19885186">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Protactinium_trihydride</td>
    <td>https://en.wikipedia.org/wiki/Protactinium_trihydride</td>
    <td><a href="https://scholia.toolforge.org/Q20165305">protactinium trihydride</a> (<a href="http://www.wikidata.org/entity/Q20165305">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Protactinium_nitride</td>
    <td>https://en.wikipedia.org/wiki/Protactinium_nitride</td>
    <td><a href="https://scholia.toolforge.org/Q20165307">Protactinium nitride</a> (<a href="http://www.wikidata.org/entity/Q20165307">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Zinc_pyrithione</td>
    <td>https://en.wikipedia.org/wiki/Zinc_pyrithione</td>
    <td><a href="https://scholia.toolforge.org/Q204602">pyrithione zinc</a> (<a href="http://www.wikidata.org/entity/Q204602">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Tin(IV)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Tin(IV)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q204994">tin(IV) fluoride</a> (<a href="http://www.wikidata.org/entity/Q204994">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Zirconium(III)_iodide</td>
    <td>https://en.wikipedia.org/wiki/Zirconium(III)_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q205624">zirconium(III) iodide</a> (<a href="http://www.wikidata.org/entity/Q205624">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Zirconium_tungstate</td>
    <td>https://en.wikipedia.org/wiki/Zirconium_tungstate</td>
    <td><a href="https://scholia.toolforge.org/Q205661">zirconium tungstate</a> (<a href="http://www.wikidata.org/entity/Q205661">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Thallium_triiodide</td>
    <td>https://en.wikipedia.org/wiki/Thallium_triiodide</td>
    <td><a href="https://scholia.toolforge.org/Q2059737">thallium triiodide</a> (<a href="http://www.wikidata.org/entity/Q2059737">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Pectic_acid</td>
    <td>https://en.wikipedia.org/wiki/Pectic_acid</td>
    <td><a href="https://scholia.toolforge.org/Q2069698">pectic acid</a> (<a href="http://www.wikidata.org/entity/Q2069698">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Plutonium(III)_bromide</td>
    <td>https://en.wikipedia.org/wiki/Plutonium(III)_bromide</td>
    <td><a href="https://scholia.toolforge.org/Q2099796">plutonium(III) bromide</a> (<a href="http://www.wikidata.org/entity/Q2099796">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Plutonium(III)_iodide</td>
    <td>https://en.wikipedia.org/wiki/Plutonium(III)_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q2099802">plutonium(III) iodide</a> (<a href="http://www.wikidata.org/entity/Q2099802">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Diborane(2)</td>
    <td>https://en.wikipedia.org/wiki/Diborane(2)</td>
    <td><a href="https://scholia.toolforge.org/Q21178092">diborane(2)</a> (<a href="http://www.wikidata.org/entity/Q21178092">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Palladium_on_carbon</td>
    <td>https://en.wikipedia.org/wiki/Palladium_on_carbon</td>
    <td><a href="https://scholia.toolforge.org/Q2185009">palladium on carbon</a> (<a href="http://www.wikidata.org/entity/Q2185009">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/PEDOT-TMA</td>
    <td>https://en.wikipedia.org/wiki/PEDOT-TMA</td>
    <td><a href="https://scholia.toolforge.org/Q2219589">PEDOT-TMA</a> (<a href="http://www.wikidata.org/entity/Q2219589">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Iron(III)_acetate</td>
    <td>https://en.wikipedia.org/wiki/Iron(III)_acetate</td>
    <td><a href="https://scholia.toolforge.org/Q2230936">basic iron(III) acetate</a> (<a href="http://www.wikidata.org/entity/Q2230936">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Carboxyhemoglobin</td>
    <td>https://en.wikipedia.org/wiki/Carboxyhemoglobin</td>
    <td><a href="https://scholia.toolforge.org/Q2259181">carboxyhemoglobin</a> (<a href="http://www.wikidata.org/entity/Q2259181">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Platinum_fulminate</td>
    <td>https://en.wikipedia.org/wiki/Platinum_fulminate</td>
    <td><a href="https://scholia.toolforge.org/Q22907796">Platinum fulminate</a> (<a href="http://www.wikidata.org/entity/Q22907796">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Rhodium-platinum_oxide</td>
    <td>https://en.wikipedia.org/wiki/Rhodium-platinum_oxide</td>
    <td><a href="https://scholia.toolforge.org/Q22908317">Rhodium-platinum oxide</a> (<a href="http://www.wikidata.org/entity/Q22908317">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ytterbium_dirhodium_disilicide</td>
    <td>https://en.wikipedia.org/wiki/Ytterbium_dirhodium_disilicide</td>
    <td><a href="https://scholia.toolforge.org/Q22909879">ytterbium dirhodium disilicide</a> (<a href="http://www.wikidata.org/entity/Q22909879">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Lithium_superoxide</td>
    <td>https://en.wikipedia.org/wiki/Lithium_superoxide</td>
    <td><a href="https://scholia.toolforge.org/Q2293867">lithium superoxide</a> (<a href="http://www.wikidata.org/entity/Q2293867">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Niobium_carbide</td>
    <td>https://en.wikipedia.org/wiki/Niobium_carbide</td>
    <td><a href="https://scholia.toolforge.org/Q2348776">niobium carbide</a> (<a href="http://www.wikidata.org/entity/Q2348776">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Phosphatidylserine</td>
    <td>https://en.wikipedia.org/wiki/Phosphatidylserine</td>
    <td><a href="https://scholia.toolforge.org/Q2354337">phosphatidyl serine</a> (<a href="http://www.wikidata.org/entity/Q2354337">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Iridium_tetrafluoride</td>
    <td>https://en.wikipedia.org/wiki/Iridium_tetrafluoride</td>
    <td><a href="https://scholia.toolforge.org/Q2356808">iridium tetrafluoride</a> (<a href="http://www.wikidata.org/entity/Q2356808">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Tetrakis(1-norbornyl)cobalt(IV)</td>
    <td>https://en.wikipedia.org/wiki/Tetrakis(1-norbornyl)cobalt(IV)</td>
    <td><a href="https://scholia.toolforge.org/Q2406745">tetrakis(1-norbornyl)cobalt(IV)</a> (<a href="http://www.wikidata.org/entity/Q2406745">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Singlet_oxygen</td>
    <td>https://en.wikipedia.org/wiki/Singlet_oxygen</td>
    <td><a href="https://scholia.toolforge.org/Q2413613">singlet oxygen</a> (<a href="http://www.wikidata.org/entity/Q2413613">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Positronium_hydride</td>
    <td>https://en.wikipedia.org/wiki/Positronium_hydride</td>
    <td><a href="https://scholia.toolforge.org/Q2419386">positronium hydride</a> (<a href="http://www.wikidata.org/entity/Q2419386">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Calcium_monophosphide</td>
    <td>https://en.wikipedia.org/wiki/Calcium_monophosphide</td>
    <td><a href="https://scholia.toolforge.org/Q2452235">calcium monophosphide</a> (<a href="http://www.wikidata.org/entity/Q2452235">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Hexol</td>
    <td>https://en.wikipedia.org/wiki/Hexol</td>
    <td><a href="https://scholia.toolforge.org/Q2462786">hexol</a> (<a href="http://www.wikidata.org/entity/Q2462786">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Holmium_monosulfide</td>
    <td>https://en.wikipedia.org/wiki/Holmium_monosulfide</td>
    <td><a href="https://scholia.toolforge.org/Q24629066">holmium sulfide</a> (<a href="http://www.wikidata.org/entity/Q24629066">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Samarium_monosulfide</td>
    <td>https://en.wikipedia.org/wiki/Samarium_monosulfide</td>
    <td><a href="https://scholia.toolforge.org/Q24629125">Samarium monosulfide</a> (<a href="http://www.wikidata.org/entity/Q24629125">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Zirconium_dichloride</td>
    <td>https://en.wikipedia.org/wiki/Zirconium_dichloride</td>
    <td><a href="https://scholia.toolforge.org/Q24629321">zirconium dichloride</a> (<a href="http://www.wikidata.org/entity/Q24629321">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ammonium_hexabromoselenate(IV)</td>
    <td>https://en.wikipedia.org/wiki/Ammonium_hexabromoselenate(IV)</td>
    <td><a href="https://scholia.toolforge.org/Q24629360">Ammonium hexabromoselenate(IV)</a> (<a href="http://www.wikidata.org/entity/Q24629360">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ammonium_hexachloroselenate(IV)</td>
    <td>https://en.wikipedia.org/wiki/Ammonium_hexachloroselenate(IV)</td>
    <td><a href="https://scholia.toolforge.org/Q24629363">Ammonium hexachloroselenate</a> (<a href="http://www.wikidata.org/entity/Q24629363">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Chromium(III)_selenide</td>
    <td>https://en.wikipedia.org/wiki/Chromium(III)_selenide</td>
    <td><a href="https://scholia.toolforge.org/Q24629453">Chromium(III) selenide</a> (<a href="http://www.wikidata.org/entity/Q24629453">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Erbium(III)_selenide</td>
    <td>https://en.wikipedia.org/wiki/Erbium(III)_selenide</td>
    <td><a href="https://scholia.toolforge.org/Q24629475">Erbium selenide</a> (<a href="http://www.wikidata.org/entity/Q24629475">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Thorium_diselenide</td>
    <td>https://en.wikipedia.org/wiki/Thorium_diselenide</td>
    <td><a href="https://scholia.toolforge.org/Q24629617">Thorium diselenide</a> (<a href="http://www.wikidata.org/entity/Q24629617">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Thulium(III)_selenide</td>
    <td>https://en.wikipedia.org/wiki/Thulium(III)_selenide</td>
    <td><a href="https://scholia.toolforge.org/Q24629645">Thulium selenide</a> (<a href="http://www.wikidata.org/entity/Q24629645">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dysprosium_monosulfide</td>
    <td>https://en.wikipedia.org/wiki/Dysprosium_monosulfide</td>
    <td><a href="https://scholia.toolforge.org/Q24629840">Dysprosium monosulfide</a> (<a href="http://www.wikidata.org/entity/Q24629840">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Gadolinium_monosulfide</td>
    <td>https://en.wikipedia.org/wiki/Gadolinium_monosulfide</td>
    <td><a href="https://scholia.toolforge.org/Q24629869">Gadolinium monosulfide</a> (<a href="http://www.wikidata.org/entity/Q24629869">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Propylene_glycol_alginate</td>
    <td>https://en.wikipedia.org/wiki/Propylene_glycol_alginate</td>
    <td><a href="https://scholia.toolforge.org/Q2474785">propylene glycol alginate</a> (<a href="http://www.wikidata.org/entity/Q2474785">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Rhenium_trioxynitrate</td>
    <td>https://en.wikipedia.org/wiki/Rhenium_trioxynitrate</td>
    <td><a href="https://scholia.toolforge.org/Q24833964">rhenium trioxide nitrate</a> (<a href="http://www.wikidata.org/entity/Q24833964">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Titanium_perchlorate</td>
    <td>https://en.wikipedia.org/wiki/Titanium_perchlorate</td>
    <td><a href="https://scholia.toolforge.org/Q24836734">titanium perchlorate</a> (<a href="http://www.wikidata.org/entity/Q24836734">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Tetramethylammonium_auride</td>
    <td>https://en.wikipedia.org/wiki/Tetramethylammonium_auride</td>
    <td><a href="https://scholia.toolforge.org/Q24836885">tetramethylammonium auride</a> (<a href="http://www.wikidata.org/entity/Q24836885">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Aurosilane</td>
    <td>https://en.wikipedia.org/wiki/Aurosilane</td>
    <td><a href="https://scholia.toolforge.org/Q24836893">Silicon tetraauride</a> (<a href="http://www.wikidata.org/entity/Q24836893">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Nickel_succinate</td>
    <td>https://en.wikipedia.org/wiki/Nickel_succinate</td>
    <td><a href="https://scholia.toolforge.org/Q24883812">nickel succinate</a> (<a href="http://www.wikidata.org/entity/Q24883812">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Bismuth_titanate</td>
    <td>https://en.wikipedia.org/wiki/Bismuth_titanate</td>
    <td><a href="https://scholia.toolforge.org/Q25055622">bismuth titanate</a> (<a href="http://www.wikidata.org/entity/Q25055622">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Lanthanum_ytterbium_oxide</td>
    <td>https://en.wikipedia.org/wiki/Lanthanum_ytterbium_oxide</td>
    <td><a href="https://scholia.toolforge.org/Q25056625">Lanthanum ytterbium oxide</a> (<a href="http://www.wikidata.org/entity/Q25056625">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/(Benzylideneacetone)iron_tricarbonyl</td>
    <td>https://en.wikipedia.org/wiki/(Benzylideneacetone)iron_tricarbonyl</td>
    <td><a href="https://scholia.toolforge.org/Q2613093">(benzylideneacetone)iron tricarbonyl</a> (<a href="http://www.wikidata.org/entity/Q2613093">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Lead(IV)_sulfide</td>
    <td>https://en.wikipedia.org/wiki/Lead(IV)_sulfide</td>
    <td><a href="https://scholia.toolforge.org/Q2613693">lead(IV) sulfide</a> (<a href="http://www.wikidata.org/entity/Q2613693">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Chlorophyll_c</td>
    <td>https://en.wikipedia.org/wiki/Chlorophyll_c1</td>
    <td><a href="https://scholia.toolforge.org/Q2620265">chlorophyll c1</a> (<a href="http://www.wikidata.org/entity/Q2620265">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Graphane</td>
    <td>https://en.wikipedia.org/wiki/Graphane</td>
    <td><a href="https://scholia.toolforge.org/Q2660535">graphane</a> (<a href="http://www.wikidata.org/entity/Q2660535">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Lithium_hexafluorosilicate</td>
    <td>https://en.wikipedia.org/wiki/Lithium_hexafluorosilicate</td>
    <td><a href="https://scholia.toolforge.org/Q27921277">lithium hexafluorosilicate</a> (<a href="http://www.wikidata.org/entity/Q27921277">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Acetylated_distarch_adipate</td>
    <td>https://en.wikipedia.org/wiki/Acetylated_distarch_adipate</td>
    <td><a href="https://scholia.toolforge.org/Q2824457">acetylated distarch adipate</a> (<a href="http://www.wikidata.org/entity/Q2824457">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Iridium_tetroxide</td>
    <td>https://en.wikipedia.org/wiki/Iridium_tetroxide</td>
    <td><a href="https://scholia.toolforge.org/Q2858011">iridium tetroxide</a> (<a href="http://www.wikidata.org/entity/Q2858011">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Radium_carbonate</td>
    <td>https://en.wikipedia.org/wiki/Radium_carbonate</td>
    <td><a href="https://scholia.toolforge.org/Q28771566">radium carbonate</a> (<a href="http://www.wikidata.org/entity/Q28771566">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Radium_oxide</td>
    <td>https://en.wikipedia.org/wiki/Radium_oxide</td>
    <td><a href="https://scholia.toolforge.org/Q28771573">radium oxide</a> (<a href="http://www.wikidata.org/entity/Q28771573">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Bismuth_phosphide</td>
    <td>https://en.wikipedia.org/wiki/Bismuth_phosphide</td>
    <td><a href="https://scholia.toolforge.org/Q28790590">bismuth phosphide</a> (<a href="http://www.wikidata.org/entity/Q28790590">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dimanganese_decacarbonyl</td>
    <td>https://en.wikipedia.org/wiki/Dimanganese_decacarbonyl</td>
    <td><a href="https://scholia.toolforge.org/Q2984452">dimanganese decacarbonyl</a> (<a href="http://www.wikidata.org/entity/Q2984452">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dicarbonyltris(triphenylphosphine)ruthenium(0)</td>
    <td>https://en.wikipedia.org/wiki/Dicarbonyltris(triphenylphosphine)ruthenium(0)</td>
    <td><a href="https://scholia.toolforge.org/Q2990492">dicarbonyltris(triphenylphosphine)ruthenium(0)</a> (<a href="http://www.wikidata.org/entity/Q2990492">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Protonated_hydrogen_cyanide</td>
    <td>https://en.wikipedia.org/wiki/Protonated_hydrogen_cyanide</td>
    <td><a href="https://scholia.toolforge.org/Q3008064">protonated hydrogen cyanide</a> (<a href="http://www.wikidata.org/entity/Q3008064">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cellulose_diacetate</td>
    <td>https://en.wikipedia.org/wiki/Cellulose_diacetate</td>
    <td><a href="https://scholia.toolforge.org/Q3025842">cellulose diacetate</a> (<a href="http://www.wikidata.org/entity/Q3025842">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dioxygenyl</td>
    <td>https://en.wikipedia.org/wiki/Dioxygenyl</td>
    <td><a href="https://scholia.toolforge.org/Q3028855">dioxygenyl ion</a> (<a href="http://www.wikidata.org/entity/Q3028855">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Gallocatechol</td>
    <td>https://en.wikipedia.org/wiki/Gallocatechol</td>
    <td><a href="https://scholia.toolforge.org/Q3044728">gallocatechol</a> (<a href="http://www.wikidata.org/entity/Q3044728">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Bismuth_ferrite</td>
    <td>https://en.wikipedia.org/wiki/Bismuth_ferrite</td>
    <td><a href="https://scholia.toolforge.org/Q3069714">bismuth ferrite</a> (<a href="http://www.wikidata.org/entity/Q3069714">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Actinium(III)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Actinium(III)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q3074510">actinium fluoride</a> (<a href="http://www.wikidata.org/entity/Q3074510">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Phosphatidylinositol_(3,4,5)-trisphosphate</td>
    <td>https://en.wikipedia.org/wiki/Phosphatidylinositol_(3,4,5)-trisphosphate</td>
    <td><a href="https://scholia.toolforge.org/Q3078767">Phosphatidylinositol (3,4,5)-trisphosphate</a> (<a href="http://www.wikidata.org/entity/Q3078767">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ammonium_tetrathiovanadate</td>
    <td>https://en.wikipedia.org/wiki/Ammonium_tetrathiovanadate</td>
    <td><a href="https://scholia.toolforge.org/Q30947886">ammonium tetrathiovanadate</a> (<a href="http://www.wikidata.org/entity/Q30947886">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Actinium(III)_iodide</td>
    <td>https://en.wikipedia.org/wiki/Actinium(III)_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q3154067">actinium triiodide</a> (<a href="http://www.wikidata.org/entity/Q3154067">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Uranium_nitrides</td>
    <td>https://en.wikipedia.org/wiki/Uranium_nitrides</td>
    <td><a href="https://scholia.toolforge.org/Q3181207">diuranium trinitride</a> (<a href="http://www.wikidata.org/entity/Q3181207">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Disodium_tetracarbonylferrate</td>
    <td>https://en.wikipedia.org/wiki/Disodium_tetracarbonylferrate</td>
    <td><a href="https://scholia.toolforge.org/Q3271014">disodium tetracarbonylferrate</a> (<a href="http://www.wikidata.org/entity/Q3271014">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Plutonium_nitride</td>
    <td>https://en.wikipedia.org/wiki/Plutonium_nitride</td>
    <td><a href="https://scholia.toolforge.org/Q3342228">plutonium nitride</a> (<a href="http://www.wikidata.org/entity/Q3342228">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Chlorinated_polyvinyl_chloride</td>
    <td>https://en.wikipedia.org/wiki/Chlorinated_polyvinyl_chloride</td>
    <td><a href="https://scholia.toolforge.org/Q3395510">chlorinated polyvinyl chloride</a> (<a href="http://www.wikidata.org/entity/Q3395510">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cadmium_hydride</td>
    <td>https://en.wikipedia.org/wiki/Cadmium_hydride</td>
    <td><a href="https://scholia.toolforge.org/Q3462573">cadmium hydride</a> (<a href="http://www.wikidata.org/entity/Q3462573">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Triplet_oxygen</td>
    <td>https://en.wikipedia.org/wiki/Triplet_oxygen</td>
    <td><a href="https://scholia.toolforge.org/Q3497595">triplet oxygen</a> (<a href="http://www.wikidata.org/entity/Q3497595">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Actinium(III)_sulfide</td>
    <td>https://en.wikipedia.org/wiki/Actinium(III)_sulfide</td>
    <td><a href="https://scholia.toolforge.org/Q3539686">actinium(III) sulfide</a> (<a href="http://www.wikidata.org/entity/Q3539686">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dichlorine_pentoxide</td>
    <td>https://en.wikipedia.org/wiki/Dichlorine_pentoxide</td>
    <td><a href="https://scholia.toolforge.org/Q3617460">dichlorine pentoxide</a> (<a href="http://www.wikidata.org/entity/Q3617460">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Chlorotoxin</td>
    <td>https://en.wikipedia.org/wiki/Chlorotoxin</td>
    <td><a href="https://scholia.toolforge.org/Q3680957">chlorotoxin</a> (<a href="http://www.wikidata.org/entity/Q3680957">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dimethyldioctadecylammonium_bromide</td>
    <td>https://en.wikipedia.org/wiki/Dimethyldioctadecylammonium_bromide</td>
    <td><a href="https://scholia.toolforge.org/Q3700517">DODAB</a> (<a href="http://www.wikidata.org/entity/Q3700517">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Tungsten(III)_oxide</td>
    <td>https://en.wikipedia.org/wiki/Tungsten(III)_oxide</td>
    <td><a href="https://scholia.toolforge.org/Q379014">tungsten(III) oxide</a> (<a href="http://www.wikidata.org/entity/Q379014">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Triiron_dodecacarbonyl</td>
    <td>https://en.wikipedia.org/wiki/Triiron_dodecacarbonyl</td>
    <td><a href="https://scholia.toolforge.org/Q382703">triiron dodecacarbonyl</a> (<a href="http://www.wikidata.org/entity/Q382703">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Terbium_silicide</td>
    <td>https://en.wikipedia.org/wiki/Terbium_silicide</td>
    <td><a href="https://scholia.toolforge.org/Q3867223">terbium silicide</a> (<a href="http://www.wikidata.org/entity/Q3867223">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Peroxomonosulfate</td>
    <td>https://en.wikipedia.org/wiki/Peroxomonosulfate</td>
    <td><a href="https://scholia.toolforge.org/Q3900055">peroxomonosulfate</a> (<a href="http://www.wikidata.org/entity/Q3900055">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Tungsten_diarsenide</td>
    <td>https://en.wikipedia.org/wiki/Tungsten_diarsenide</td>
    <td><a href="https://scholia.toolforge.org/Q4069954">tungsten(VI) arsenide</a> (<a href="http://www.wikidata.org/entity/Q4069954">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Yttrium_acetylacetonate</td>
    <td>https://en.wikipedia.org/wiki/Yttrium_acetylacetonate</td>
    <td><a href="https://scholia.toolforge.org/Q4073298">yttrium acetylacetonate</a> (<a href="http://www.wikidata.org/entity/Q4073298">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Scandium_acetylacetonate</td>
    <td>https://en.wikipedia.org/wiki/Scandium_acetylacetonate</td>
    <td><a href="https://scholia.toolforge.org/Q4073301">scandium acetylacetonate</a> (<a href="http://www.wikidata.org/entity/Q4073301">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Methylaluminoxane</td>
    <td>https://en.wikipedia.org/wiki/Methylaluminoxane</td>
    <td><a href="https://scholia.toolforge.org/Q408080">methylaluminoxane</a> (<a href="http://www.wikidata.org/entity/Q408080">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Titanium_aluminide</td>
    <td>https://en.wikipedia.org/wiki/Titanium_aluminide</td>
    <td><a href="https://scholia.toolforge.org/Q408746">titanium aluminide</a> (<a href="http://www.wikidata.org/entity/Q408746">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Acid_Red_13</td>
    <td>https://en.wikipedia.org/wiki/Acid_red_13</td>
    <td><a href="https://scholia.toolforge.org/Q40888254">Acid Red 13</a> (<a href="http://www.wikidata.org/entity/Q40888254">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Lithium_hexafluorogermanate</td>
    <td>https://en.wikipedia.org/wiki/Lithium_hexafluorogermanate</td>
    <td><a href="https://scholia.toolforge.org/Q40889202">Lithium hexafluorogermanate</a> (<a href="http://www.wikidata.org/entity/Q40889202">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Indium(I)_bromide</td>
    <td>https://en.wikipedia.org/wiki/Indium(I)_bromide</td>
    <td><a href="https://scholia.toolforge.org/Q4096880">indium(I) bromide</a> (<a href="http://www.wikidata.org/entity/Q4096880">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Boron_suboxide</td>
    <td>https://en.wikipedia.org/wiki/Boron_suboxide</td>
    <td><a href="https://scholia.toolforge.org/Q4120057">Boron suboxide</a> (<a href="http://www.wikidata.org/entity/Q4120057">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Polylactic_acid</td>
    <td>https://en.wikipedia.org/wiki/Polylactic_acid</td>
    <td><a href="https://scholia.toolforge.org/Q413769">polylactic acid</a> (<a href="http://www.wikidata.org/entity/Q413769">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Strontium_hydride</td>
    <td>https://en.wikipedia.org/wiki/Strontium_hydride</td>
    <td><a href="https://scholia.toolforge.org/Q4138050">strontium hydride</a> (<a href="http://www.wikidata.org/entity/Q4138050">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Actinium(III)_hydroxide</td>
    <td>https://en.wikipedia.org/wiki/Actinium(III)_hydroxide</td>
    <td><a href="https://scholia.toolforge.org/Q4138095">actinium hydroxide</a> (<a href="http://www.wikidata.org/entity/Q4138095">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Radium_hydroxide</td>
    <td>https://en.wikipedia.org/wiki/Radium_hydroxide</td>
    <td><a href="https://scholia.toolforge.org/Q4138111">radium hydroxide</a> (<a href="http://www.wikidata.org/entity/Q4138111">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Nisin</td>
    <td>https://en.wikipedia.org/wiki/Nisin</td>
    <td><a href="https://scholia.toolforge.org/Q415798">nisin</a> (<a href="http://www.wikidata.org/entity/Q415798">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Polyacrylamide</td>
    <td>https://en.wikipedia.org/wiki/Polyacrylamide</td>
    <td><a href="https://scholia.toolforge.org/Q416002">polyacrylamide</a> (<a href="http://www.wikidata.org/entity/Q416002">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cobalt(II)_hydride</td>
    <td>https://en.wikipedia.org/wiki/Cobalt(II)_hydride</td>
    <td><a href="https://scholia.toolforge.org/Q4161299">cobalt(II) hydride</a> (<a href="http://www.wikidata.org/entity/Q4161299">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Molybdenum_dichloride_dioxide</td>
    <td>https://en.wikipedia.org/wiki/Molybdenum_dichloride_dioxide</td>
    <td><a href="https://scholia.toolforge.org/Q4161974">molybdenum dichloride dioxide</a> (<a href="http://www.wikidata.org/entity/Q4161974">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Collins_reagent</td>
    <td>https://en.wikipedia.org/wiki/Collins_reagent</td>
    <td><a href="https://scholia.toolforge.org/Q416217">Collins reagent</a> (<a href="http://www.wikidata.org/entity/Q416217">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Molybdenum_diphosphide</td>
    <td>https://en.wikipedia.org/wiki/Molybdenum_diphosphide</td>
    <td><a href="https://scholia.toolforge.org/Q4162492">Molybdenum diphosphide</a> (<a href="http://www.wikidata.org/entity/Q4162492">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cobalt_green</td>
    <td>https://en.wikipedia.org/wiki/Cobalt_green</td>
    <td><a href="https://scholia.toolforge.org/Q416459">cobalt green</a> (<a href="http://www.wikidata.org/entity/Q416459">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Silver_subfluoride</td>
    <td>https://en.wikipedia.org/wiki/Silver_subfluoride</td>
    <td><a href="https://scholia.toolforge.org/Q417478">silver subfluoride</a> (<a href="http://www.wikidata.org/entity/Q417478">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Radium_iodate</td>
    <td>https://en.wikipedia.org/wiki/Radium_iodate</td>
    <td><a href="https://scholia.toolforge.org/Q4202638">cesium arsenate</a> (<a href="http://www.wikidata.org/entity/Q4202638">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Radium_iodide</td>
    <td>https://en.wikipedia.org/wiki/Radium_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q4202665">radium(II) iodide</a> (<a href="http://www.wikidata.org/entity/Q4202665">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Xenon_hexafluoroplatinate</td>
    <td>https://en.wikipedia.org/wiki/Xenon_hexafluoroplatinate</td>
    <td><a href="https://scholia.toolforge.org/Q420831">xenon hexafluoroplatinate</a> (<a href="http://www.wikidata.org/entity/Q420831">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ruthenium_red</td>
    <td>https://en.wikipedia.org/wiki/Ruthenium_red</td>
    <td><a href="https://scholia.toolforge.org/Q424006">ruthenium red</a> (<a href="http://www.wikidata.org/entity/Q424006">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Tantalum_hafnium_carbide</td>
    <td>https://en.wikipedia.org/wiki/Tantalum_hafnium_carbide</td>
    <td><a href="https://scholia.toolforge.org/Q424268">tantalum hafnium carbide</a> (<a href="http://www.wikidata.org/entity/Q424268">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Polyvinyl_butyral</td>
    <td>https://en.wikipedia.org/wiki/Polyvinyl_butyral</td>
    <td><a href="https://scholia.toolforge.org/Q424631">polyvinyl butyral</a> (<a href="http://www.wikidata.org/entity/Q424631">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Maitotoxin</td>
    <td>https://en.wikipedia.org/wiki/Maitotoxin</td>
    <td><a href="https://scholia.toolforge.org/Q425072">maitotoxin</a> (<a href="http://www.wikidata.org/entity/Q425072">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Rhenium_diboride</td>
    <td>https://en.wikipedia.org/wiki/Rhenium_diboride</td>
    <td><a href="https://scholia.toolforge.org/Q425164">rhenium diboride</a> (<a href="http://www.wikidata.org/entity/Q425164">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Brown_FK</td>
    <td>https://en.wikipedia.org/wiki/Brown_FK</td>
    <td><a href="https://scholia.toolforge.org/Q425437">brown FK</a> (<a href="http://www.wikidata.org/entity/Q425437">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Tantalum_carbide</td>
    <td>https://en.wikipedia.org/wiki/Tantalum_carbide</td>
    <td><a href="https://scholia.toolforge.org/Q426498">tantalum carbide</a> (<a href="http://www.wikidata.org/entity/Q426498">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Actinium(III)_nitrate</td>
    <td>https://en.wikipedia.org/wiki/Actinium(III)_nitrate</td>
    <td><a href="https://scholia.toolforge.org/Q4321577">actinium(III) nitrate</a> (<a href="http://www.wikidata.org/entity/Q4321577">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cadmium_nitride</td>
    <td>https://en.wikipedia.org/wiki/Cadmium_nitride</td>
    <td><a href="https://scholia.toolforge.org/Q4321616">cadmium nitride</a> (<a href="http://www.wikidata.org/entity/Q4321616">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Rubidium_ozonide</td>
    <td>https://en.wikipedia.org/wiki/Rubidium_ozonide</td>
    <td><a href="https://scholia.toolforge.org/Q4332243">rubidium ozonide</a> (<a href="http://www.wikidata.org/entity/Q4332243">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Yttrium_oxyfluoride</td>
    <td>https://en.wikipedia.org/wiki/Yttrium_oxyfluoride</td>
    <td><a href="https://scholia.toolforge.org/Q4332915">yttrium oxyfluoride</a> (<a href="http://www.wikidata.org/entity/Q4332915">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Lanthanum_oxyfluoride</td>
    <td>https://en.wikipedia.org/wiki/Lanthanum_oxyfluoride</td>
    <td><a href="https://scholia.toolforge.org/Q4332916">Lanthanum oxyfluoride</a> (<a href="http://www.wikidata.org/entity/Q4332916">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Actinium(III)_phosphate</td>
    <td>https://en.wikipedia.org/wiki/Actinium(III)_phosphate</td>
    <td><a href="https://scholia.toolforge.org/Q4337162">actinium(III) orthophosphate</a> (<a href="http://www.wikidata.org/entity/Q4337162">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Rubidium_peroxide</td>
    <td>https://en.wikipedia.org/wiki/Rubidium_peroxide</td>
    <td><a href="https://scholia.toolforge.org/Q4351683">rubidium peroxide</a> (<a href="http://www.wikidata.org/entity/Q4351683">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Caesium_peroxide</td>
    <td>https://en.wikipedia.org/wiki/Caesium_peroxide</td>
    <td><a href="https://scholia.toolforge.org/Q4351685">cesium peroxide</a> (<a href="http://www.wikidata.org/entity/Q4351685">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dicobalt_silicide</td>
    <td>https://en.wikipedia.org/wiki/Dicobalt_silicide</td>
    <td><a href="https://scholia.toolforge.org/Q4419230">Dicobalt silicide</a> (<a href="http://www.wikidata.org/entity/Q4419230">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cobalt_monosilicide</td>
    <td>https://en.wikipedia.org/wiki/Cobalt_monosilicide</td>
    <td><a href="https://scholia.toolforge.org/Q4419233">cobalt monosilicide</a> (<a href="http://www.wikidata.org/entity/Q4419233">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Manganese_monosilicide</td>
    <td>https://en.wikipedia.org/wiki/Manganese_monosilicide</td>
    <td><a href="https://scholia.toolforge.org/Q4419236">manganese monosilicide</a> (<a href="http://www.wikidata.org/entity/Q4419236">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Polonium(IV)_sulfate</td>
    <td>https://en.wikipedia.org/wiki/Polonium(IV)_sulfate</td>
    <td><a href="https://scholia.toolforge.org/Q4445813">polonium(IV) sulfate</a> (<a href="http://www.wikidata.org/entity/Q4445813">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Radium_sulfate</td>
    <td>https://en.wikipedia.org/wiki/Radium_sulfate</td>
    <td><a href="https://scholia.toolforge.org/Q4445816">radium sulfate</a> (<a href="http://www.wikidata.org/entity/Q4445816">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Osmium_tetrasulfide</td>
    <td>https://en.wikipedia.org/wiki/Osmium_tetrasulfide</td>
    <td><a href="https://scholia.toolforge.org/Q4445863">osmium(VIII) sulfide</a> (<a href="http://www.wikidata.org/entity/Q4445863">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Technetium(VII)_sulfide</td>
    <td>https://en.wikipedia.org/wiki/Technetium(VII)_sulfide</td>
    <td><a href="https://scholia.toolforge.org/Q4445881">technetium(VII) sulfide</a> (<a href="http://www.wikidata.org/entity/Q4445881">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Titanium(III)_sulfide</td>
    <td>https://en.wikipedia.org/wiki/Titanium(III)_sulfide</td>
    <td><a href="https://scholia.toolforge.org/Q4445883">titanium sulfide</a> (<a href="http://www.wikidata.org/entity/Q4445883">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Diarsenic_tetraiodide</td>
    <td>https://en.wikipedia.org/wiki/Diarsenic_tetraiodide</td>
    <td><a href="https://scholia.toolforge.org/Q4456626">arsenic diiodide</a> (<a href="http://www.wikidata.org/entity/Q4456626">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Nitratoauric_acid</td>
    <td>https://en.wikipedia.org/wiki/Nitratoauric_acid</td>
    <td><a href="https://scholia.toolforge.org/Q4456639">gold(III) hydrogen nitrate</a> (<a href="http://www.wikidata.org/entity/Q4456639">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ferrovanadium</td>
    <td>https://en.wikipedia.org/wiki/Ferrovanadium</td>
    <td><a href="https://scholia.toolforge.org/Q4483127">ferrovanadium</a> (<a href="http://www.wikidata.org/entity/Q4483127">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Trimolybdenum_phosphide</td>
    <td>https://en.wikipedia.org/wiki/Trimolybdenum_phosphide</td>
    <td><a href="https://scholia.toolforge.org/Q4492133">Trimolybdenum phosphide</a> (<a href="http://www.wikidata.org/entity/Q4492133">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Caesium_phosphide</td>
    <td>https://en.wikipedia.org/wiki/Caesium_phosphide</td>
    <td><a href="https://scholia.toolforge.org/Q4492135">Caesium phosphide</a> (<a href="http://www.wikidata.org/entity/Q4492135">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Osmium(IV)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Osmium(IV)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q4493218">osmium(IV) fluoride</a> (<a href="http://www.wikidata.org/entity/Q4493218">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Osmium_octafluoride</td>
    <td>https://en.wikipedia.org/wiki/Osmium_octafluoride</td>
    <td><a href="https://scholia.toolforge.org/Q4493219">osmium(VIII) fluoride</a> (<a href="http://www.wikidata.org/entity/Q4493219">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Protactinium(V)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Protactinium(V)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q4493226">protactinium(V) fluoride</a> (<a href="http://www.wikidata.org/entity/Q4493226">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Tungsten(II)_chloride</td>
    <td>https://en.wikipedia.org/wiki/Tungsten(II)_chloride</td>
    <td><a href="https://scholia.toolforge.org/Q4498197">tungsten(II) chloride</a> (<a href="http://www.wikidata.org/entity/Q4498197">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Iridium(II)_chloride</td>
    <td>https://en.wikipedia.org/wiki/Iridium(II)_chloride</td>
    <td><a href="https://scholia.toolforge.org/Q4498213">iridium(II) chloride</a> (<a href="http://www.wikidata.org/entity/Q4498213">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Acetylferrocene</td>
    <td>https://en.wikipedia.org/wiki/Acetylferrocene</td>
    <td><a href="https://scholia.toolforge.org/Q4673312">acetylferrocene</a> (<a href="http://www.wikidata.org/entity/Q4673312">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Americium(III)_bromide</td>
    <td>https://en.wikipedia.org/wiki/Americium(III)_bromide</td>
    <td><a href="https://scholia.toolforge.org/Q467634">americium(III) bromide</a> (<a href="http://www.wikidata.org/entity/Q467634">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Americium(III)_iodide</td>
    <td>https://en.wikipedia.org/wiki/Americium(III)_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q467656">americium(III) iodide</a> (<a href="http://www.wikidata.org/entity/Q467656">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Adenosine_thiamine_diphosphate</td>
    <td>https://en.wikipedia.org/wiki/Adenosine_thiamine_diphosphate</td>
    <td><a href="https://scholia.toolforge.org/Q4682284">Adenosine thiamine diphosphate</a> (<a href="http://www.wikidata.org/entity/Q4682284">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Shvo_catalyst</td>
    <td>https://en.wikipedia.org/wiki/Shvo_catalyst</td>
    <td><a href="https://scholia.toolforge.org/Q4788036">Shvo catalyst</a> (<a href="http://www.wikidata.org/entity/Q4788036">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Beryllium_azide</td>
    <td>https://en.wikipedia.org/wiki/Beryllium_azide</td>
    <td><a href="https://scholia.toolforge.org/Q4896099">beryllium azide</a> (<a href="http://www.wikidata.org/entity/Q4896099">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Bismuth_silicon_oxide</td>
    <td>https://en.wikipedia.org/wiki/Bismuth_silicon_oxide</td>
    <td><a href="https://scholia.toolforge.org/Q4918352">bismuth silicon oxide</a> (<a href="http://www.wikidata.org/entity/Q4918352">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cadmium(I)_tetrachloroaluminate</td>
    <td>https://en.wikipedia.org/wiki/Cadmium(I)_tetrachloroaluminate</td>
    <td><a href="https://scholia.toolforge.org/Q5016546">cadmium(I) tetrachloroaluminate</a> (<a href="http://www.wikidata.org/entity/Q5016546">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Caesium_cadmium_bromide</td>
    <td>https://en.wikipedia.org/wiki/Caesium_cadmium_bromide</td>
    <td><a href="https://scholia.toolforge.org/Q5017045">caesium cadmium bromide</a> (<a href="http://www.wikidata.org/entity/Q5017045">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Caesium_cadmium_chloride</td>
    <td>https://en.wikipedia.org/wiki/Caesium_cadmium_chloride</td>
    <td><a href="https://scholia.toolforge.org/Q5017047">caesium cadmium chloride</a> (<a href="http://www.wikidata.org/entity/Q5017047">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Caesium_dodecaborate</td>
    <td>https://en.wikipedia.org/wiki/Caesium_dodecaborate</td>
    <td><a href="https://scholia.toolforge.org/Q5017048">caesium dodecaborate</a> (<a href="http://www.wikidata.org/entity/Q5017048">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Caesium_hexafluorocobaltate(IV)</td>
    <td>https://en.wikipedia.org/wiki/Caesium_hexafluorocobaltate(IV)</td>
    <td><a href="https://scholia.toolforge.org/Q5017049">caesium hexafluorocobaltate(IV)</a> (<a href="http://www.wikidata.org/entity/Q5017049">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Caesium_lithium_borate</td>
    <td>https://en.wikipedia.org/wiki/Caesium_lithium_borate</td>
    <td><a href="https://scholia.toolforge.org/Q5017050">caesium lithium borate</a> (<a href="http://www.wikidata.org/entity/Q5017050">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Caesium_hexafluorocuprate(IV)</td>
    <td>https://en.wikipedia.org/wiki/Caesium_hexafluorocuprate(IV)</td>
    <td><a href="https://scholia.toolforge.org/Q5017051">caesium hexafluorocuprate(IV)</a> (<a href="http://www.wikidata.org/entity/Q5017051">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Calcium_copper_titanate</td>
    <td>https://en.wikipedia.org/wiki/Calcium_copper_titanate</td>
    <td><a href="https://scholia.toolforge.org/Q5018824">Calcium copper titanate</a> (<a href="http://www.wikidata.org/entity/Q5018824">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Chlorine_tetroxide</td>
    <td>https://en.wikipedia.org/wiki/Chlorine_tetroxide</td>
    <td><a href="https://scholia.toolforge.org/Q5102956">chlorine tetroxide</a> (<a href="http://www.wikidata.org/entity/Q5102956">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Chloro(cyclopentadienyl)bis(triphenylphosphine)ruthenium</td>
    <td>https://en.wikipedia.org/wiki/Chloro(cyclopentadienyl)bis(triphenylphosphine)ruthenium</td>
    <td><a href="https://scholia.toolforge.org/Q5102986">chloro(cyclopentadienyl)bis(triphenylphosphine)ruthenium</a> (<a href="http://www.wikidata.org/entity/Q5102986">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Chloro(tetrahydrothiophene)gold(I)</td>
    <td>https://en.wikipedia.org/wiki/Chloro(tetrahydrothiophene)gold(I)</td>
    <td><a href="https://scholia.toolforge.org/Q5102989">chloro(tetrahydrothiophene)gold(I)</a> (<a href="http://www.wikidata.org/entity/Q5102989">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Chromium(I)_hydride</td>
    <td>https://en.wikipedia.org/wiki/Chromium(I)_hydride</td>
    <td><a href="https://scholia.toolforge.org/Q5113812">Chromium(I) hydride</a> (<a href="http://www.wikidata.org/entity/Q5113812">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Chromium(II)_hydride</td>
    <td>https://en.wikipedia.org/wiki/Chromium(II)_hydride</td>
    <td><a href="https://scholia.toolforge.org/Q5113814">chromium(II) hydride</a> (<a href="http://www.wikidata.org/entity/Q5113814">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Chromium_acetate_hydroxide</td>
    <td>https://en.wikipedia.org/wiki/Chromium_acetate_hydroxide</td>
    <td><a href="https://scholia.toolforge.org/Q5113827">chromium acetate hydroxide</a> (<a href="http://www.wikidata.org/entity/Q5113827">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Tetramethylammonium_pentafluoroxenate</td>
    <td>https://en.wikipedia.org/wiki/Tetramethylammonium_pentafluoroxenate</td>
    <td><a href="https://scholia.toolforge.org/Q511638">tetramethylammonium pentafluoroxenate</a> (<a href="http://www.wikidata.org/entity/Q511638">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cinchotannic_acid</td>
    <td>https://en.wikipedia.org/wiki/Cinchotannic_acid</td>
    <td><a href="https://scholia.toolforge.org/Q5120194">Cinchotannic acid</a> (<a href="http://www.wikidata.org/entity/Q5120194">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cobatoxin</td>
    <td>https://en.wikipedia.org/wiki/Cobatoxin</td>
    <td><a href="https://scholia.toolforge.org/Q5138732">Cobatoxin</a> (<a href="http://www.wikidata.org/entity/Q5138732">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Digallane</td>
    <td>https://en.wikipedia.org/wiki/Digallane</td>
    <td><a href="https://scholia.toolforge.org/Q516785">digallane</a> (<a href="http://www.wikidata.org/entity/Q516785">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Copper_ibuprofenate</td>
    <td>https://en.wikipedia.org/wiki/Copper_ibuprofenate</td>
    <td><a href="https://scholia.toolforge.org/Q5168779">Copper ibuprofenate</a> (<a href="http://www.wikidata.org/entity/Q5168779">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cyclobutadieneiron_tricarbonyl</td>
    <td>https://en.wikipedia.org/wiki/Cyclobutadieneiron_tricarbonyl</td>
    <td><a href="https://scholia.toolforge.org/Q5198676">Cyclobutadieneiron tricarbonyl</a> (<a href="http://www.wikidata.org/entity/Q5198676">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cyclooctatetraenide_anion</td>
    <td>https://en.wikipedia.org/wiki/Cyclooctatetraenide_anion</td>
    <td><a href="https://scholia.toolforge.org/Q5198907">cyclooctatetraenide anion</a> (<a href="http://www.wikidata.org/entity/Q5198907">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cyclopentadienylcobalt_dicarbonyl</td>
    <td>https://en.wikipedia.org/wiki/Cyclopentadienylcobalt_dicarbonyl</td>
    <td><a href="https://scholia.toolforge.org/Q5198926">cyclopentadienylcobalt dicarbonyl</a> (<a href="http://www.wikidata.org/entity/Q5198926">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cyclopentadienyl_allyl_palladium</td>
    <td>https://en.wikipedia.org/wiki/Cyclopentadienyl_allyl_palladium</td>
    <td><a href="https://scholia.toolforge.org/Q5198927">cyclopentadienyl allyl palladium</a> (<a href="http://www.wikidata.org/entity/Q5198927">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cyclopentadienyliron_dicarbonyl_iodide</td>
    <td>https://en.wikipedia.org/wiki/Cyclopentadienyliron_dicarbonyl_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q5198928">Cyclopentadienyliron dicarbonyl iodide</a> (<a href="http://www.wikidata.org/entity/Q5198928">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/DEAE-Sepharose</td>
    <td>https://en.wikipedia.org/wiki/DEAE-Sepharose</td>
    <td><a href="https://scholia.toolforge.org/Q5204759">DEAE-Sepharose</a> (<a href="http://www.wikidata.org/entity/Q5204759">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Decamethyldizincocene</td>
    <td>https://en.wikipedia.org/wiki/Decamethyldizincocene</td>
    <td><a href="https://scholia.toolforge.org/Q5248734">Decamethyldizincocene</a> (<a href="http://www.wikidata.org/entity/Q5248734">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dichlorobis(ethylenediamine)nickel(II)</td>
    <td>https://en.wikipedia.org/wiki/Dichlorobis(ethylenediamine)nickel(II)</td>
    <td><a href="https://scholia.toolforge.org/Q5272477">Dichlorobis(ethylenediamine)nickel(II)</a> (<a href="http://www.wikidata.org/entity/Q5272477">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ditungsten_tetra(hpp)</td>
    <td>https://en.wikipedia.org/wiki/Ditungsten_tetra(hpp)</td>
    <td><a href="https://scholia.toolforge.org/Q5283737">Ditungsten tetra(hpp)</a> (<a href="http://www.wikidata.org/entity/Q5283737">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dodecacalcium_hepta-aluminate</td>
    <td>https://en.wikipedia.org/wiki/Dodecacalcium_hepta-aluminate</td>
    <td><a href="https://scholia.toolforge.org/Q5287801">Dodecacalcium hepta-aluminate</a> (<a href="http://www.wikidata.org/entity/Q5287801">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Epicutissimin_A</td>
    <td>https://en.wikipedia.org/wiki/Epicutissimin_A</td>
    <td><a href="https://scholia.toolforge.org/Q5382668">Epicutissimin A</a> (<a href="http://www.wikidata.org/entity/Q5382668">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Gallium_maltolate</td>
    <td>https://en.wikipedia.org/wiki/Gallium_maltolate</td>
    <td><a href="https://scholia.toolforge.org/Q5519111">Gallium maltolate</a> (<a href="http://www.wikidata.org/entity/Q5519111">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ferrichrome_A</td>
    <td>https://en.wikipedia.org/wiki/Ferrichrome_A</td>
    <td><a href="https://scholia.toolforge.org/Q55286742">Ferrichrome A</a> (<a href="http://www.wikidata.org/entity/Q55286742">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Glyceryl_hydroxystearate</td>
    <td>https://en.wikipedia.org/wiki/Glyceryl_hydroxystearate</td>
    <td><a href="https://scholia.toolforge.org/Q5572569">glyceryl hydroxystearate</a> (<a href="http://www.wikidata.org/entity/Q5572569">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Glycine_propionyl-L-carnitine</td>
    <td>https://en.wikipedia.org/wiki/Glycine_propionyl-L-carnitine</td>
    <td><a href="https://scholia.toolforge.org/Q5572581">Glycine propionyl-l-carnitine</a> (<a href="http://www.wikidata.org/entity/Q5572581">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Gold_heptafluoride</td>
    <td>https://en.wikipedia.org/wiki/Gold_heptafluoride</td>
    <td><a href="https://scholia.toolforge.org/Q5578934">gold heptafluoride</a> (<a href="http://www.wikidata.org/entity/Q5578934">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Vanadium(III)_acetylacetonate</td>
    <td>https://en.wikipedia.org/wiki/Vanadium(III)_acetylacetonate</td>
    <td><a href="https://scholia.toolforge.org/Q56605537">vanadium(III) acetylacetonate</a> (<a href="http://www.wikidata.org/entity/Q56605537">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dysprosium_titanate</td>
    <td>https://en.wikipedia.org/wiki/Dysprosium_titanate</td>
    <td><a href="https://scholia.toolforge.org/Q577230">dysprosium(III) titanate</a> (<a href="http://www.wikidata.org/entity/Q577230">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ruthenium(III)_acetate</td>
    <td>https://en.wikipedia.org/wiki/Ruthenium(III)_acetate</td>
    <td><a href="https://scholia.toolforge.org/Q59197074">ruthenium(III) acetate</a> (<a href="http://www.wikidata.org/entity/Q59197074">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/(Pentamethylcyclopentadienyl)aluminium(I)</td>
    <td>https://en.wikipedia.org/wiki/(Pentamethylcyclopentadienyl)aluminium(I)</td>
    <td><a href="https://scholia.toolforge.org/Q59284842">(pentamethylcyclopentadienyl)aluminium(I)</a> (<a href="http://www.wikidata.org/entity/Q59284842">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Scandium_dodecaboride</td>
    <td>https://en.wikipedia.org/wiki/Scandium_dodecaboride</td>
    <td><a href="https://scholia.toolforge.org/Q6129106">scandium dodecaboride</a> (<a href="http://www.wikidata.org/entity/Q6129106">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Curdlan</td>
    <td>https://en.wikipedia.org/wiki/Curdlan</td>
    <td><a href="https://scholia.toolforge.org/Q616242">curdlan</a> (<a href="http://www.wikidata.org/entity/Q616242">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Kinotannic_acid</td>
    <td>https://en.wikipedia.org/wiki/Kinotannic_acid</td>
    <td><a href="https://scholia.toolforge.org/Q6414206">Kinotannic acid</a> (<a href="http://www.wikidata.org/entity/Q6414206">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Kryptonium_ion</td>
    <td>https://en.wikipedia.org/wiki/Kryptonium_ion</td>
    <td><a href="https://scholia.toolforge.org/Q6439721">kryptonium ion</a> (<a href="http://www.wikidata.org/entity/Q6439721">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Thulium(II)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Thulium(II)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q65051115">thulium difluoride</a> (<a href="http://www.wikidata.org/entity/Q65051115">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cyclopentadienyl_magnesium_bromide</td>
    <td>https://en.wikipedia.org/wiki/Cyclopentadienyl_magnesium_bromide</td>
    <td><a href="https://scholia.toolforge.org/Q65062358">Cyclopentadienyl magnesium bromide</a> (<a href="http://www.wikidata.org/entity/Q65062358">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Bilirubin_glucuronide</td>
    <td>https://en.wikipedia.org/wiki/Bilirubin_glucuronide</td>
    <td><a href="https://scholia.toolforge.org/Q65067489">Bilirubin glucuronide</a> (<a href="http://www.wikidata.org/entity/Q65067489">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Leumorphin</td>
    <td>https://en.wikipedia.org/wiki/Leumorphin</td>
    <td><a href="https://scholia.toolforge.org/Q6534550">Leumorphin</a> (<a href="http://www.wikidata.org/entity/Q6534550">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Cobratoxin</td>
    <td>https://en.wikipedia.org/wiki/Cobratoxin</td>
    <td><a href="https://scholia.toolforge.org/Q661977">cobratoxin</a> (<a href="http://www.wikidata.org/entity/Q661977">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Magnesium_aluminide</td>
    <td>https://en.wikipedia.org/wiki/Magnesium_aluminide</td>
    <td><a href="https://scholia.toolforge.org/Q6731377">Magnesium aluminide</a> (<a href="http://www.wikidata.org/entity/Q6731377">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Magnesium_nickel_hydride</td>
    <td>https://en.wikipedia.org/wiki/Magnesium_nickel_hydride</td>
    <td><a href="https://scholia.toolforge.org/Q6731397">Magnesium nickel hydride</a> (<a href="http://www.wikidata.org/entity/Q6731397">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Magnesium_polonide</td>
    <td>https://en.wikipedia.org/wiki/Magnesium_polonide</td>
    <td><a href="https://scholia.toolforge.org/Q6731402">magnesium polonide</a> (<a href="http://www.wikidata.org/entity/Q6731402">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Mercury(IV)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Mercury(IV)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q6818562">mercury(IV) fluoride</a> (<a href="http://www.wikidata.org/entity/Q6818562">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Merrilactone_A</td>
    <td>https://en.wikipedia.org/wiki/Merrilactone_A</td>
    <td><a href="https://scholia.toolforge.org/Q6820147">Merrilactone A</a> (<a href="http://www.wikidata.org/entity/Q6820147">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Methanetetracarboxylate</td>
    <td>https://en.wikipedia.org/wiki/Methanetetracarboxylate</td>
    <td><a href="https://scholia.toolforge.org/Q6823572">methanetetracarboxylate</a> (<a href="http://www.wikidata.org/entity/Q6823572">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Methylvanillylecgonine</td>
    <td>https://en.wikipedia.org/wiki/Methylvanillylecgonine</td>
    <td><a href="https://scholia.toolforge.org/Q6824067">Methylvanillylecgonine</a> (<a href="http://www.wikidata.org/entity/Q6824067">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Mutacin_1140</td>
    <td>https://en.wikipedia.org/wiki/Mutacin_1140</td>
    <td><a href="https://scholia.toolforge.org/Q6943638">mutacin 1140</a> (<a href="http://www.wikidata.org/entity/Q6943638">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/NBD-TMA</td>
    <td>https://en.wikipedia.org/wiki/NBD-TMA</td>
    <td><a href="https://scholia.toolforge.org/Q6952803">NBD-TMA</a> (<a href="http://www.wikidata.org/entity/Q6952803">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/NR58-3.14.3</td>
    <td>https://en.wikipedia.org/wiki/NR58-3.14.3</td>
    <td><a href="https://scholia.toolforge.org/Q6955100">NR58-3.14.3</a> (<a href="http://www.wikidata.org/entity/Q6955100">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Urodilatin</td>
    <td>https://en.wikipedia.org/wiki/Urodilatin</td>
    <td><a href="https://scholia.toolforge.org/Q6961789">Ularitide</a> (<a href="http://www.wikidata.org/entity/Q6961789">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Nitrogen_pentafluoride</td>
    <td>https://en.wikipedia.org/wiki/Nitrogen_pentafluoride</td>
    <td><a href="https://scholia.toolforge.org/Q7041476">nitrogen pentafluoride</a> (<a href="http://www.wikidata.org/entity/Q7041476">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Pentaamminenitritocobalt(III)_chloride</td>
    <td>https://en.wikipedia.org/wiki/Pentaamminenitritocobalt(III)_chloride</td>
    <td><a href="https://scholia.toolforge.org/Q7041490">nitropentaamminecobalt(III) chloride</a> (<a href="http://www.wikidata.org/entity/Q7041490">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Nitronium_perchlorate</td>
    <td>https://en.wikipedia.org/wiki/Nitronium_perchlorate</td>
    <td><a href="https://scholia.toolforge.org/Q7041493">nitronium perchlorate</a> (<a href="http://www.wikidata.org/entity/Q7041493">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/OUP-16</td>
    <td>https://en.wikipedia.org/wiki/OUP-16</td>
    <td><a href="https://scholia.toolforge.org/Q7073136">OUP-16</a> (<a href="http://www.wikidata.org/entity/Q7073136">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Octadecaborane</td>
    <td>https://en.wikipedia.org/wiki/Octadecaborane</td>
    <td><a href="https://scholia.toolforge.org/Q7076687">Octadecaborane</a> (<a href="http://www.wikidata.org/entity/Q7076687">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Palladium_tetrafluoride</td>
    <td>https://en.wikipedia.org/wiki/Palladium_tetrafluoride</td>
    <td><a href="https://scholia.toolforge.org/Q7127719">palladium tetrafluoride</a> (<a href="http://www.wikidata.org/entity/Q7127719">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Pentaamine(dinitrogen)ruthenium(II)_chloride</td>
    <td>https://en.wikipedia.org/wiki/Pentaamine(dinitrogen)ruthenium(II)_chloride</td>
    <td><a href="https://scholia.toolforge.org/Q7164918">pentaamine(dinitrogen)ruthenium(II) chloride</a> (<a href="http://www.wikidata.org/entity/Q7164918">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Phosphatrioxa-adamantane</td>
    <td>https://en.wikipedia.org/wiki/Phosphatrioxa-adamantane</td>
    <td><a href="https://scholia.toolforge.org/Q7187470">Phosphatrioxa-adamantane</a> (<a href="http://www.wikidata.org/entity/Q7187470">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Pinotin_A</td>
    <td>https://en.wikipedia.org/wiki/Pinotin_A</td>
    <td><a href="https://scholia.toolforge.org/Q7196417">pinotin A</a> (<a href="http://www.wikidata.org/entity/Q7196417">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Platinum(II)_acetate</td>
    <td>https://en.wikipedia.org/wiki/Platinum(II)_acetate</td>
    <td><a href="https://scholia.toolforge.org/Q7202319">platinum(II) acetate</a> (<a href="http://www.wikidata.org/entity/Q7202319">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Pleuran</td>
    <td>https://en.wikipedia.org/wiki/Pleuran</td>
    <td><a href="https://scholia.toolforge.org/Q7204737">pleuran</a> (<a href="http://www.wikidata.org/entity/Q7204737">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Polonium_monoxide</td>
    <td>https://en.wikipedia.org/wiki/Polonium_monoxide</td>
    <td><a href="https://scholia.toolforge.org/Q7225950">polonium monoxide</a> (<a href="http://www.wikidata.org/entity/Q7225950">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Polonium_trioxide</td>
    <td>https://en.wikipedia.org/wiki/Polonium_trioxide</td>
    <td><a href="https://scholia.toolforge.org/Q7225951">polonium trioxide</a> (<a href="http://www.wikidata.org/entity/Q7225951">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Poloxamer_407</td>
    <td>https://en.wikipedia.org/wiki/Poloxamer_407</td>
    <td><a href="https://scholia.toolforge.org/Q7225971">Poloxamer 407</a> (<a href="http://www.wikidata.org/entity/Q7225971">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Polyaminopropyl_biguanide</td>
    <td>https://en.wikipedia.org/wiki/Polyaminopropyl_biguanide</td>
    <td><a href="https://scholia.toolforge.org/Q7226132">polyaminopropyl biguanide</a> (<a href="http://www.wikidata.org/entity/Q7226132">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Polydioctylfluorene</td>
    <td>https://en.wikipedia.org/wiki/Polydioctylfluorene</td>
    <td><a href="https://scholia.toolforge.org/Q7226282">Polydioctylfluorene</a> (<a href="http://www.wikidata.org/entity/Q7226282">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Polyhydroxyethylmethacrylate</td>
    <td>https://en.wikipedia.org/wiki/Polyhydroxyethylmethacrylate</td>
    <td><a href="https://scholia.toolforge.org/Q7226502">polyhydroxyethylmethacrylate</a> (<a href="http://www.wikidata.org/entity/Q7226502">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Polysilicone-15</td>
    <td>https://en.wikipedia.org/wiki/Polysilicone-15</td>
    <td><a href="https://scholia.toolforge.org/Q7226938">Polysilicone-15</a> (<a href="http://www.wikidata.org/entity/Q7226938">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Potassium_dideuterium_phosphate</td>
    <td>https://en.wikipedia.org/wiki/Potassium_dideuterium_phosphate</td>
    <td><a href="https://scholia.toolforge.org/Q7234693">potassium dideuterium phosphate</a> (<a href="http://www.wikidata.org/entity/Q7234693">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Potassium_erythorbate</td>
    <td>https://en.wikipedia.org/wiki/Potassium_erythorbate</td>
    <td><a href="https://scholia.toolforge.org/Q7234694">potassium erythorbate</a> (<a href="http://www.wikidata.org/entity/Q7234694">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Potassium_dimanganate(III)</td>
    <td>https://en.wikipedia.org/wiki/Potassium_dimanganate(III)</td>
    <td><a href="https://scholia.toolforge.org/Q7234696">potassium dimanganate(III)</a> (<a href="http://www.wikidata.org/entity/Q7234696">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Psymberin</td>
    <td>https://en.wikipedia.org/wiki/Psymberin</td>
    <td><a href="https://scholia.toolforge.org/Q7256580">psymberin</a> (<a href="http://www.wikidata.org/entity/Q7256580">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Punicacortein_D</td>
    <td>https://en.wikipedia.org/wiki/Punicacortein_D</td>
    <td><a href="https://scholia.toolforge.org/Q7260200">punicacortein D</a> (<a href="http://www.wikidata.org/entity/Q7260200">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Raspberry_ellagitannin</td>
    <td>https://en.wikipedia.org/wiki/Raspberry_ellagitannin</td>
    <td><a href="https://scholia.toolforge.org/Q7295197">Raspberry ellagitannin</a> (<a href="http://www.wikidata.org/entity/Q7295197">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Scandium_monosulfide</td>
    <td>https://en.wikipedia.org/wiki/Scandium_monosulfide</td>
    <td><a href="https://scholia.toolforge.org/Q7429991">scandium monosulfide</a> (<a href="http://www.wikidata.org/entity/Q7429991">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Stenophyllanin_A</td>
    <td>https://en.wikipedia.org/wiki/Stenophyllanin_A</td>
    <td><a href="https://scholia.toolforge.org/Q7607715">Stenophyllanin A</a> (<a href="http://www.wikidata.org/entity/Q7607715">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Distrontium_ruthenate</td>
    <td>https://en.wikipedia.org/wiki/Distrontium_ruthenate</td>
    <td><a href="https://scholia.toolforge.org/Q7624778">strontium ruthenate</a> (<a href="http://www.wikidata.org/entity/Q7624778">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/TME_(psychedelics)</td>
    <td>https://en.wikipedia.org/wiki/TME_(psychedelics)</td>
    <td><a href="https://scholia.toolforge.org/Q7670729">TME</a> (<a href="http://www.wikidata.org/entity/Q7670729">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Tellurium_monoiodide</td>
    <td>https://en.wikipedia.org/wiki/Tellurium_monoiodide</td>
    <td><a href="https://scholia.toolforge.org/Q7697690">tellurium(I) iodide</a> (<a href="http://www.wikidata.org/entity/Q7697690">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Nitrostarch</td>
    <td>https://en.wikipedia.org/wiki/Nitrostarch</td>
    <td><a href="https://scholia.toolforge.org/Q774946">nitrostarch</a> (<a href="http://www.wikidata.org/entity/Q774946">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Sodium_polonide</td>
    <td>https://en.wikipedia.org/wiki/Sodium_polonide</td>
    <td><a href="https://scholia.toolforge.org/Q7788974">sodium polonide</a> (<a href="http://www.wikidata.org/entity/Q7788974">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Lithium_polonide</td>
    <td>https://en.wikipedia.org/wiki/Lithium_polonide</td>
    <td><a href="https://scholia.toolforge.org/Q7789180">lithium polonide</a> (<a href="http://www.wikidata.org/entity/Q7789180">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Trimethylenemethane</td>
    <td>https://en.wikipedia.org/wiki/Trimethylenemethane</td>
    <td><a href="https://scholia.toolforge.org/Q7842213">trimethylenemethane</a> (<a href="http://www.wikidata.org/entity/Q7842213">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Vanillotoxin</td>
    <td>https://en.wikipedia.org/wiki/Vanillotoxin</td>
    <td><a href="https://scholia.toolforge.org/Q7914938">Vanillotoxin</a> (<a href="http://www.wikidata.org/entity/Q7914938">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Xenon_dichloride</td>
    <td>https://en.wikipedia.org/wiki/Xenon_dichloride</td>
    <td><a href="https://scholia.toolforge.org/Q8043632">xenon dichloride</a> (<a href="http://www.wikidata.org/entity/Q8043632">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Xenon_hexafluororhodate</td>
    <td>https://en.wikipedia.org/wiki/Xenon_hexafluororhodate</td>
    <td><a href="https://scholia.toolforge.org/Q8043633">xenon hexafluororhodate</a> (<a href="http://www.wikidata.org/entity/Q8043633">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Xenonium</td>
    <td>https://en.wikipedia.org/wiki/Xenonium</td>
    <td><a href="https://scholia.toolforge.org/Q8043637">xenonium ion</a> (<a href="http://www.wikidata.org/entity/Q8043637">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Xylitol_pentanitrate</td>
    <td>https://en.wikipedia.org/wiki/Xylitol_pentanitrate</td>
    <td><a href="https://scholia.toolforge.org/Q8045413">Xylitol pentanitrate</a> (<a href="http://www.wikidata.org/entity/Q8045413">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Zinc_L-aspartate</td>
    <td>https://en.wikipedia.org/wiki/Zinc_L-aspartate</td>
    <td><a href="https://scholia.toolforge.org/Q8072280">zinc L-aspartate</a> (<a href="http://www.wikidata.org/entity/Q8072280">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Zinc_borate</td>
    <td>https://en.wikipedia.org/wiki/Zinc_borate</td>
    <td><a href="https://scholia.toolforge.org/Q8072284">zinc borate</a> (<a href="http://www.wikidata.org/entity/Q8072284">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Zinc_chloride_hydroxide_monohydrate</td>
    <td>https://en.wikipedia.org/wiki/Zinc_chloride_hydroxide_monohydrate</td>
    <td><a href="https://scholia.toolforge.org/Q8072293">zinc chloride hydroxide monohydrate</a> (<a href="http://www.wikidata.org/entity/Q8072293">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Zirconium_propionate</td>
    <td>https://en.wikipedia.org/wiki/Zirconium_propionate</td>
    <td><a href="https://scholia.toolforge.org/Q8072754">Zirconium propanoate</a> (<a href="http://www.wikidata.org/entity/Q8072754">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Berkelium(III)_bromide</td>
    <td>https://en.wikipedia.org/wiki/Berkelium(III)_bromide</td>
    <td><a href="https://scholia.toolforge.org/Q820864">berkelium(III) bromide</a> (<a href="http://www.wikidata.org/entity/Q820864">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Berkelium(III)_chloride</td>
    <td>https://en.wikipedia.org/wiki/Berkelium(III)_chloride</td>
    <td><a href="https://scholia.toolforge.org/Q820865">berkelium(III) chloride</a> (<a href="http://www.wikidata.org/entity/Q820865">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Berkelium(III)_fluoride</td>
    <td>https://en.wikipedia.org/wiki/Berkelium(III)_fluoride</td>
    <td><a href="https://scholia.toolforge.org/Q820870">berkelium(III) fluoride</a> (<a href="http://www.wikidata.org/entity/Q820870">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Berkelium(III)_iodide</td>
    <td>https://en.wikipedia.org/wiki/Berkelium(III)_iodide</td>
    <td><a href="https://scholia.toolforge.org/Q820871">berkelium(III) iodide</a> (<a href="http://www.wikidata.org/entity/Q820871">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Berkelium(IV)_oxide</td>
    <td>https://en.wikipedia.org/wiki/Berkelium(IV)_oxide</td>
    <td><a href="https://scholia.toolforge.org/Q820876">berkelium(IV) oxide</a> (<a href="http://www.wikidata.org/entity/Q820876">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Berkelium(III)_oxide</td>
    <td>https://en.wikipedia.org/wiki/Berkelium(III)_oxide</td>
    <td><a href="https://scholia.toolforge.org/Q820878">berkelium(III) oxide</a> (<a href="http://www.wikidata.org/entity/Q820878">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dibromodiethyl_sulfoxide</td>
    <td>https://en.wikipedia.org/wiki/Dibromodiethyl_sulfoxide</td>
    <td><a href="https://scholia.toolforge.org/Q82722915">Dibromodiethyl sulfoxide</a> (<a href="http://www.wikidata.org/entity/Q82722915">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ammonium_hexachlorotellurate</td>
    <td>https://en.wikipedia.org/wiki/Ammonium_hexachlorotellurate</td>
    <td><a href="https://scholia.toolforge.org/Q82913785">Ammonium hexachlorotellurate(IV)</a> (<a href="http://www.wikidata.org/entity/Q82913785">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Copper(II)_cyanurate</td>
    <td>https://en.wikipedia.org/wiki/Copper(II)_cyanurate</td>
    <td><a href="https://scholia.toolforge.org/Q85754040">Copper(II) cyanurate</a> (<a href="http://www.wikidata.org/entity/Q85754040">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dibenzylaniline</td>
    <td>https://en.wikipedia.org/wiki/Dibenzylaniline</td>
    <td><a href="https://scholia.toolforge.org/Q85756789">Dibenzylaniline</a> (<a href="http://www.wikidata.org/entity/Q85756789">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dibromodiethyl_sulfide</td>
    <td>https://en.wikipedia.org/wiki/Dibromodiethyl_sulfide</td>
    <td><a href="https://scholia.toolforge.org/Q85756798">Dibromodiethyl sulfide</a> (<a href="http://www.wikidata.org/entity/Q85756798">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Boron_arsenide</td>
    <td>https://en.wikipedia.org/wiki/Boron_arsenide</td>
    <td><a href="https://scholia.toolforge.org/Q866825">boron arsenide</a> (<a href="http://www.wikidata.org/entity/Q866825">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Lithopone</td>
    <td>https://en.wikipedia.org/wiki/Lithopone</td>
    <td><a href="https://scholia.toolforge.org/Q899314">Lithopone</a> (<a href="http://www.wikidata.org/entity/Q899314">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Californium(III)_oxychloride</td>
    <td>https://en.wikipedia.org/wiki/Californium(III)_oxychloride</td>
    <td><a href="https://scholia.toolforge.org/Q904529">californium oxychloride</a> (<a href="http://www.wikidata.org/entity/Q904529">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Chrysolaminarin</td>
    <td>https://en.wikipedia.org/wiki/Chrysolaminarin</td>
    <td><a href="https://scholia.toolforge.org/Q906080">chrysolaminarin</a> (<a href="http://www.wikidata.org/entity/Q906080">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Gallium_phosphate</td>
    <td>https://en.wikipedia.org/wiki/Gallium_phosphate</td>
    <td><a href="https://scholia.toolforge.org/Q906969">gallium phosphate</a> (<a href="http://www.wikidata.org/entity/Q906969">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/ADDA_(amino_acid)</td>
    <td>https://en.wikipedia.org/wiki/ADDA_(amino_acid)</td>
    <td><a href="https://scholia.toolforge.org/Q9137074">ADDA</a> (<a href="http://www.wikidata.org/entity/Q9137074">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Ammonium_alginate</td>
    <td>https://en.wikipedia.org/wiki/Ammonium_alginate</td>
    <td><a href="https://scholia.toolforge.org/Q9147958">ammonium alginate</a> (<a href="http://www.wikidata.org/entity/Q9147958">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Carbon_monofluoride</td>
    <td>https://en.wikipedia.org/wiki/Carbon_monofluoride</td>
    <td><a href="https://scholia.toolforge.org/Q947047">carbon monofluoride</a> (<a href="http://www.wikidata.org/entity/Q947047">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Aluminium_monohydroxide</td>
    <td>https://en.wikipedia.org/wiki/Aluminium_monohydroxide</td>
    <td><a href="https://scholia.toolforge.org/Q97163408">hydroxyaluminium(I)</a> (<a href="http://www.wikidata.org/entity/Q97163408">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Indium(II)_selenide</td>
    <td>https://en.wikipedia.org/wiki/Indium(II)_selenide</td>
    <td><a href="https://scholia.toolforge.org/Q971847">indium(II) selenide</a> (<a href="http://www.wikidata.org/entity/Q971847">edit</a>)</td>
  </tr>
  <tr>
    <td>http://dbpedia.org/resource/Dibromine_pentoxide</td>
    <td>https://en.wikipedia.org/wiki/Dibromine_pentoxide</td>
    <td><a href="https://scholia.toolforge.org/Q977125">dibromine pentoxide</a> (<a href="http://www.wikidata.org/entity/Q977125">edit</a>)</td>
  </tr>
</table>
## Code examples
### curl
```shell
curl -o missingSMILES.rq https://raw.githubusercontent.com/egonw/SARS-CoV-2-Queries/master/sparql/missingSMILES.rq
curl -H "Accept: text/tab-separated-values" -G https://query.wikidata.org/bigdata/namespace/wdq/sparql --data-urlencode query@missingSMILES.rq
```
This SPARQL query is available under CCZero.
