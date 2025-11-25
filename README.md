[route.html](https://github.com/user-attachments/files/23757811/route.html)
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>광주 청년 문화버스 보완 노선도</title>
    <script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyC_fKNo3ClLoeBiRXGkjeJ02W7wm93zNiI"></script>

    <style>
      html, body {
        height: 100%;
        margin: 0;
        padding: 0;
        font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      }
      #map {
        width: 100%;
        height: 100%;
      }
      .overlay-container {
        position: absolute;
        top: 12px;
        left: 12px;
        z-index: 10;
      }
      .map-title {
        background: rgba(255, 255, 255, 0.9);
        padding: 8px 12px;
        border-radius: 8px;
        font-size: 16px;
        font-weight: 600;
        margin-bottom: 8px;
        box-shadow: 0 2px 4px rgba(0,0,0,0.15);
      }
      .map-subtitle {
        background: rgba(255, 255, 255, 0.9);
        padding: 6px 10px;
        border-radius: 8px;
        font-size: 11px;
        box-shadow: 0 2px 4px rgba(0,0,0,0.15);
      }
      .legend {
        position: absolute;
        bottom: 12px;
        left: 12px;
        z-index: 10;
        background: rgba(255, 255, 255, 0.9);
        padding: 8px 12px;
        border-radius: 8px;
        font-size: 12px;
        box-shadow: 0 2px 4px rgba(0,0,0,0.15);
      }
      .legend-title {
        font-weight: 600;
        margin-bottom: 4px;
      }
      .legend-item {
        display: flex;
        align-items: center;
        margin-bottom: 2px;
      }
      .legend-line {
        width: 20px;
        height: 3px;
        margin-right: 6px;
        background: #0066ff;
        border-radius: 2px;
      }
      .legend-marker {
        width: 16px;
        height: 16px;
        border-radius: 50%;
        border: 2px solid #0066ff;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        font-size: 9px;
        margin-right: 6px;
        color: #0066ff;
        background: #ffffff;
      }
    </style>

    <script>
      function initMap() {
        const map = new google.maps.Map(document.getElementById("map"), {
          center: { lat: 35.1595, lng: 126.8526 }, // 광주 중심
          zoom: 13,
        });

        // 👇 보완 노선 정류장 목록 (순서대로 연결됨)
        const routeStops = [
          {
            order: 1,
            place: "전남대학교 후문",
            lat: 35.173000,
            lon: 126.909800,
            note: "청년 생활권 출발 거점"
          },
          {
            order: 2,
            place: "동명동 카페거리",
            lat: 35.150900,
            lon: 126.932900,
            note: "청년 여가·모임 공간"
          },
          {
            order: 3,
            place: "국립아시아문화전당(ACC)",
            lat: 35.146100,
            lon: 126.922600,
            note: "전시·공연 중심 문화시설"
          },
          {
            order: 4,
            place: "충장로 상권·축제거리",
            lat: 35.148400,
            lon: 126.919400,
            note: "축제·쇼핑·야간 활동 중심"
          },
          {
            order: 5,
            place: "양림동 역사문화마을",
            lat: 35.139500,
            lon: 126.912300,
            note: "역사·관광·카페 복합 명소"
          },
          {
            order: 6,
            place: "광주 비엔날레 전시관",
            lat: 35.175200,
            lon: 126.889600,
            note: "국제 전시·행사 거점"
          },
          {
            order: 7,
            place: "기아 챔피언스 필드",
            lat: 35.168940,
            lon: 126.888470,
            note: "야간 경기·대규모 인파"
          }
        ];

        // Polyline 경로 생성
        const routePath = new google.maps.Polyline({
          path: routeStops.map(stop => ({ lat: stop.lat, lng: stop.lon })),
          geodesic: true,
          strokeColor: "#0066ff",
          strokeOpacity: 0.9,
          strokeWeight: 4,
        });

        routePath.setMap(map);

        // 마커 & 인포윈도우
        const infoWindow = new google.maps.InfoWindow();

        routeStops.forEach((stop, index) => {
          const marker = new google.maps.Marker({
            position: { lat: stop.lat, lng: stop.lon },
            map,
            title: stop.place,
            label: {
              text: String(stop.order),
              color: "#ffffff",
              fontSize: "11px",
              fontWeight: "700",
            },
            icon: {
              path: google.maps.SymbolPath.CIRCLE,
              scale: 11,
              fillColor: "#0066ff",
              fillOpacity: 1,
              strokeWeight: 1,
              strokeColor: "#ffffff",
            },
          });

          const contentHtml = `
            <div style="font-size:13px;">
              <strong>${stop.order}. ${stop.place}</strong><br/>
              <span>${stop.note}</span>
            </div>
          `;

          marker.addListener("click", () => {
            infoWindow.setContent(contentHtml);
            infoWindow.open(map, marker);
          });
        });
      }
    </script>
  </head>

  <body onload="initMap()">
    <div class="overlay-container">
      <div class="map-title">
        광주 청년 문화버스 보완 노선도 (시범안)
      </div>
      <div class="map-subtitle">
        전남대 생활권에서 동명동·ACC·충장로·양림동·비엔날레·기아 챔피언스 필드를<br/>
        하나의 문화 순환 노선으로 연결하는 가상 노선입니다.
      </div>
    </div>

    <div class="legend">
      <div class="legend-title">표시 설명</div>
      <div class="legend-item">
        <span class="legend-line"></span> 제안된 청년 문화버스 이동 경로
      </div>
      <div class="legend-item">
        <span class="legend-marker">1</span> 정류장 번호 (출발 → 도착 순서)
      </div>
    </div>

    <div id="map"></div>
  </body>
</html>
