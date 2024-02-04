
	const path = require('path');
	//style-loader: 동적으로 스타일 추가 (<style> 태그로 동적 적용)
	//css-loader: css 파일을 번들링
	//url-loader: 이미지, 폰트 같은 파일을 번들링
	//image-webpack-loader 번들링 하는 동안 이미지의 크기를 줄이고 품질 향상
	//file-loader: 이미지, 폰트 같은 파일을 번들링
	
	//url-loader는 파일의 크기가 작을 때는 데이터 URL 형식으로 인라인화하여 번들에 포함시키므로 번들 크기를 줄이는 데 도움이 된다
	
	module.exports = {
	  entry: './src/index.js',  // 애플리케이션 진입점
	  output: {
	    path: path.resolve(__dirname, 'dist'),
	    filename: 'bundle.js'
	  },
	  module: {
	    rules: [
	      {
	        test: /\.css$/,
	        use: ['style-loader', 'css-loader']
	      },
	      {
	        test: /\.(png|jpe?g|gif)$/,
	        use: [
	          {
	            loader: 'url-loader',
	            options: {
	              limit: 8192, // 8KB 미만인 이미지는 Data URL로 인라인화
	              name: '[name].[contenthash].[ext]', // 파일명 유지
	              outputPath: 'images' // 이미지 출력 경로
	            }
	          },
	          {
	            loader: 'image-webpack-loader', // 이미지 최적화 로더
	            options: {
	              mozjpeg: {
	                progressive: true,
	                quality: 65
	              },
	              optipng: {
	                enabled: false
	              },
	              pngquant: {
	                quality: [0.65, 0.90],
	                speed: 4
	              },
	              gifsicle: {
	                interlaced: false
	              },
	              webp: {
	                quality: 75
	              }
	            }
	          }
	        ]
	      },
	      {
	        test: /\.mp4$/,
	        use: 'file-loader' // 또는 url-loader를 사용할 수도 있습니다.
	      }
	    ]
	  }
	};
