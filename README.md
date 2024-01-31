const path = require('path');

module.exports = {
  entry: './src/index.js', // 애플리케이션 진입점
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.(png|jpe?g|gif)$/i,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 8192, // 8KB 미만인 이미지는 Data URL로 인라인화
              name: '[name].[contenthash].[ext]', // 파일명 유지
              outputPath: 'images', // 이미지 출력 경로
            },
          },
          {
            loader: 'image-webpack-loader', // image-webpack-loader 추가
            options: {
              mozjpeg: {
                progressive: true,
                quality: 65
              },
              optipng: {
                enabled: false,
              },
              pngquant: {
                quality: [0.65, 0.90],
                speed: 4
              },
              gifsicle: {
                interlaced: false,
              },
              webp: {
                quality: 75
              }
            }
          }
        ],
      },
    ],
  },
};
