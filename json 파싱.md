```json
{
  "documents": [
    {
      "address": {
        "address_name": "서울 강남구 역삼동 736-42",
        "b_code": "1168010100",
        "h_code": "1168064000",
        "main_address_no": "736",
        "mountain_yn": "N",
        "region_1depth_name": "서울",
        "region_2depth_name": "강남구",
        "region_3depth_h_name": "역삼1동",
        "region_3depth_name": "역삼동",
        "sub_address_no": "42",
        "x": "127.035297345311",
        "y": "37.4991227916312"
      },
      "address_name": "서울 강남구 테헤란로22길 13",
      "address_type": "ROAD_ADDR",
      "road_address": {
        "address_name": "서울 강남구 테헤란로22길 13",
        "building_name": "예동빌딩",
        "main_building_no": "13",
        "region_1depth_name": "서울",
        "region_2depth_name": "강남구",
        "region_3depth_name": "역삼동",
        "road_name": "테헤란로22길",
        "sub_building_no": "",
        "underground_yn": "N",
        "x": "127.035297345311",
        "y": "37.4991227916312",
        "zone_no": "06236"
      },
      "x": "127.035297345311",
      "y": "37.4991227916312"
    }
  ],
  "meta": {
    "is_end": true,
    "pageable_count": 1,
    "total_count": 1
  }
}
```

## address 필드에서 "x", "y" 값을 받아오는 방법

```java
public List<Double> callGeoApi(String queryParam) throws JsonMappingException, JsonProcessingException {
    RestTemplate restTemplate = new RestTemplate();
    HttpHeaders headers = new HttpHeaders();
    headers.setContentType(MediaType.APPLICATION_JSON);
    headers.set("Authorization", Constants.KAKAO_API_KEY);

    HttpEntity<String> request = new HttpEntity<>(headers);

    String url = "https://dapi.kakao.com/v2/local/search/address.json";

    ResponseEntity<String> response = restTemplate.exchange(url + "?query=" + queryParam,
            HttpMethod.GET,
            request,
            String.class);

    // JSON 파싱
    ObjectMapper objectMapper = new ObjectMapper();
    JsonNode rootNode = objectMapper.readTree(response.getBody());
    JsonNode documentsNode = rootNode.path("documents");
    List<Double> coordinates = new ArrayList<>();
    if (documentsNode.isArray()) {
        Iterator<JsonNode> iterator = documentsNode.elements();
        while (iterator.hasNext()) {
            JsonNode documentNode = iterator.next();
            JsonNode addressNode = documentNode.path("address");
            if (!addressNode.isMissingNode()) {
                JsonNode xNode = addressNode.path("x");
                JsonNode yNode = addressNode.path("y");
                if (!xNode.isMissingNode() && !yNode.isMissingNode()) {
                    Double x = xNode.asDouble();
                    Double y = yNode.asDouble();
                    coordinates.add(x);
                    coordinates.add(y);
                }
            }
        }
    }
    return coordinates;
}
```

## doucment 필드에서 "x", "y" 값을 받는 방법

```java
ObjectMapper objectMapper = new ObjectMapper();
JsonNode rootNode = objectMapper.readTree(jsonString);
JsonNode documentsNode = rootNode.path("documents");
List<Double> coordinates = new ArrayList<>();
if (documentsNode.isArray()) {
    Iterator<JsonNode> iterator = documentsNode.elements();
    while (iterator.hasNext()) {
        JsonNode documentNode = iterator.next();
        JsonNode xNode = documentNode.path("x");
        JsonNode yNode = documentNode.path("y");
        if (!xNode.isMissingNode() && !yNode.isMissingNode()) {
            coordinates.add(xNode.asDouble());
            coordinates.add(yNode.asDouble());
        }
    }
}
return coordinates;
```
