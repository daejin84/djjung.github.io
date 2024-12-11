# djjung.github.io


# 2024. 12. 11. 회전 변환 관련된 내용 추가

import numpy as np
import matplotlib.pyplot as plt


def rotate_line(line, angle):
    rad = angle * np.pi / 180
    c = np.cos(rad)
    s = np.sin(rad)

    x = line[:, 0]
    y = line[:, 1]

    result = np.zeros_like(line)
    new_x = x * c - y * s
    new_y = x * s + y * c
    result[:, 0] = new_x
    result[:, 1] = new_y

    return result


def draw_line(line, color):
    plt.plot(line[:, 0], line[:, 1], color=color)


def get_distance(line):
    x = line[:, 0]
    y = line[:, 1]
    distance = np.sqrt(x*x + y*y)
    return distance


def line_interpolation(line_ref, line_comp, angle):

    # line_ref가 짧을 경우를 대비 해서 거리를 길게 만들어줌
    # line_ref를 해당 angle로 회전변환을 시켜줌
    # 각 포인트마다 거리를 구함
    # interpolation 해줌
    # 결과 리턴

    line_interp = np.zeros([1, 100])
    return line_interp


def line_error_estimation(line_ref, line_comp, angle):
    line_interp = line_interpolation(line_ref=line_ref, line_comp=line_comp, angle=angle)
    error = np.sqrt(np.sum( np.sqrt(line_comp - line_interp)))
    return error


if __name__ == '__main__':

    # 첫번재 라인 : reference line (거리상으로 조금 더 짧음)
    line_1 = np.zeros([30, 2])
    line_1[:, 1] = np.linspace(start=0, stop=98, num=30, endpoint=True)

    # 두번재 라인 : 회전된 line (거리상으로 조금 더 길다)
    line_2 = np.zeros([28, 2])
    line_2[:, 1] = np.linspace(start=0, stop=103, num=28, endpoint=True)
    line_2_30 = rotate_line(line_2, 30)

    result = line_error_estimation(line_ref=line_1, line_comp=line_2_30, angle=30)


